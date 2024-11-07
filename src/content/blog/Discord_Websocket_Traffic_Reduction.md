---
title: How Discord Reached 40% Reduction of Websocket Traffic
pubDate: Oct 25, 2024 at 15h15
author: Cormontagne Romain
tags:
  - Optimization
  - Web
  - Social Media
imgUrl: '../../assets/discord-logo.webp'
description: Over the last 6 months, Discord developers worked on an improvement of the bandwith usage of their iOS and Android clients, and managed to increase its speed by 40%. Learn here how they achieved this speed gain !
layout: '../../layouts/BlogPost.astro'
---
# How Discord Reached 40% Reduction of Websocket Traffic
---
## Context

Since the end of 2017, Discord managed to reduce the size of messages, making them from 2 to 10 times smaller using client's gateway[^1] compression through zlib[^2].

Since then, a new compression library had become more attractive : zstandard, which offers a better compression ratio and supports dictionaries, allowing preemptive exchange of compressed information, resulting in an even more increased compression ratio and the reduction of the bandwidth usage.

In 2019, testings were performed with zstandard, but they weren't conclusive. The desktop-only tests proved to use too much RAM. In 2024, however, another chance was given to the library, as the support for dictionaries combined with mostly small and well-defined payloads for the gateway had great potential.

Discord thought that predicting the payloads patterns and contents would be greatly used with dictionaries in order to reduce the bandwidth usage even further. That was the start of the experiments with the potentially better zstandard library.

The team decided to conduct a _dark launch_ of zstandard through compressing a small part of production traffic using both zlib and zstandard, collecting some metrics and then discarding the zstandard data, allowing them to compare the results of both libraries and enabling them to evaluate zstandard's performance without fully implementing support for clients (desktop, iOS, Android), which would have taken about a month. This _dark launch_ enabled them to test and iterate over a few days rather than waiting weeks for full client integration.

After setting up the experiment and deploying it onto their getaway cluster, they setup a dashboard to see zstandard performance. And when they started sending traffic through the _dark launch_ code, the results showed that zstandard was performing worse than zlib.

The comparison criteria was the compression ratio of the two libraries, which equals the ratio of the uncompressed files size with the compressed file size. To illustrate the difference between tthe two libraries, where the average size of a certain payload compressed with zlib was of 250 bytes, while the same payload compressed using zstandard reached 750 bytes in size. This happened to be a general trend, zstandard was hardly ever better than zlib. The investigations on this then started.

## Streaming zstandard

One of the key reasons behind this difference was the usage of streaming compression by zlib unlike zstandard.

Most of the payloads are very small, only a few hundred bytes, which limits zstandard's ability to optimize compression based on past data. With zlib’s streaming compression, a stream is created when the connection opens and remains active until the websocket closes. This allows zlib to use data from previously compressed messages to improve the compression of new data, resulting in smaller overall payload sizes.

Now, the team wanted to know if they would be able to apply the same concept to zstandard. However, since the gateway is written in elixir, the zstandard bindings for elixir and erlang they found didn't support streaming compression.


They eventually chose to use ezstd[^3] because it supported dictionaries. Although it didn’t initially support streaming, they forked ezstd to add streaming functionality themselves, and then contributed this improvement back to the original open-source project.

Afterwards, they re-ran the _dark launch_ using zstandard streaming, and finally obtained the desired results, with zstandard streaming outperforming zlib both in compression time **and** compression ratio.

## Pushing Further


The team still wondered how far they could push this. The initial experiments used zstandard’s default settings, and they wanted to explore how much they could increase the compression ratio by adjusting the compression settings. Here's how far they got.

### Tuning

Zstandard is highly configurable, allowing the Discord team to adjust several compression parameters. They concentrated on three that they believed would most impact compression: chainlog, hashlog, and windowlog. These parameters balance compression speed, memory usage, and compression ratio. For instance, increasing the chainlog value typically enhances the compression ratio, but it also increases memory usage and compression time.

They also wanted to make sure that the compression contexts, with the chosen settings, would still fit within the memory limits of their hosts. While adding more hosts to handle the increased memory usage is an option, it can cause additional costs and eventually leads to diminishing returns in terms of performance gains. They decided to settle for parameters values which would comfortably fit in the memory of a gate node.

### Zstandard Dictionaries

The team wanted to explore zstandard's dictionary support to further enhance compression efficiency. By pre-loading zstandard with specific information, they aimed to improve compression for the first few kilobytes of data. However, this added complexity because both the gateway (compressor) and the Discord client (decompressor) needed to have the same dictionary to function correctly.

To generate these dictionaries, they gathered and anonymized a large amount of data — 120,000 messages — splitting them between two encoding methods used by the gateway: JSON and ETF. Since a JSON dictionary wouldn’t work well with ETF and vice versa, they created two separate dictionaries for each encoding type. After generating the dictionaries using zstandard’s built-in training tool, they could test their performance without deploying the gateway cluster.

When testing dictionary compression on a large payload (around 3 MB), the dictionary provided a modest reduction — from 306,745 bytes to 306,098 bytes, only about 600 bytes saved. However, on smaller payloads of around 700 bytes, the dictionary showed more significant gains, reducing the size to 40% of its initial value. This improved performance on smaller payloads is due to zstandard's ability to leverage the preloaded dictionary before it has enough compressed data to learn from.

Encouraged by the results, especially with smaller payloads, they deployed dictionary support to their gateway cluster and continued testing, comparing zstandard with and without dictionaries using their _dark launch_ process.

They focused on a specific payload size which is one of the first messages sent over the websocket. They thought it would likely benefit the most from dictionary compression. However the compression gains for that payload were minimal. Therefore, they examined other dispatch types, hoping to see better results for smaller payloads.

Unfortunately, the outcomes were mixed. For instance, when looking at the message create payload size, they found that using the dictionary actually made the compression results worse.

Eventually, they gave up with the experiments on dictionaries, as the little compression enhancement they offered wasn't worth the added complexity.

### Buffer Upgrading

They ultimately investigated the possibility of increasing zstandard buffers during off-peak hours, as Discord's traffic follows a daily pattern where peak demand requires significantly more memory than the rest of the day.

While autoscaling the gateway cluster could help optimize resource usage during off-peak times, traditional autoscaling methods were ineffective for the long-lived gateway connections. This resulted in excess memory and compute resources during quieter periods, prompting the team to consider whether they could leverage these resources to enhance compression.

To explore this, they implemented a feedback loop within the gateway cluster. This loop monitored memory usage by connected clients and determined the percentage of new clients that should receive an upgraded zstandard buffer. Upgrading the buffer increases the windowlog, hashlog, and chainlog values by one, effectively doubling the buffer's memory usage, as these parameters are powers of two.

After deploying the feedback loop and allowing it to run, the results fell short of the expectations.

Upon further investigation, they found that memory fragmentation was a key factor causing the feedback loop to perform poorly. The feedback loop assessed real system memory usage, but BEAM (Erlang’s virtual machine) was allocating more memory than actually required to handle the connected clients. This led the feedback loop to underestimate the available memory.

To address this, the dev team experimented with tweaking the BEAM allocator settings, specifically one which manages memory for driver data allocations. The bulk of a gateway process’s memory usage comes from the zstandard streaming context, implemented in C via a _NIF_ (Native Implemented Function). Since _NIF_ memory is allocated by that specific driver, they hypothesized that optimizing its settings could reduce fragmentation and improve the upgrade ratio.

However, after some experimentation, they decided to revert the feedback loop changes. While it’s possible they could have found the right allocator settings with more effort, the complexity added to the gateway cluster and the time required to fine-tune the allocators weren't worth any potential performance gains.

### Implementations and Rollout

Although the initial plan was to use zstandard only for mobile users, the bandwidth improvements were so substantial that it was decided to deploy it to desktop users as well. Since zstandard is provided as a C library, the main task was to find appropriate bindings for each platform: Java for Android, Objective-C for iOS, and Rust for Desktop. Implementation was straightforward for Android (using zstd-jni) and Desktop (using zstd-safe), as existing bindings were available, but for iOS, it was necessary to develop new bindings.

Given the potential risks — such as rendering Discord unusable if issues arose — the rollout was gated behind an experiment. This experiment allowed the team to quickly roll back if needed, verify the results observed in testing, and assess whether the change impacted any key metrics negatively.

After a few months of testing and experimentation, zstandard was successfully deployed to all users across all platforms.

## Another Win: Passive Sessions V2


While not directly related to the zstandard project, the metrics from the _dark launch_ phase revealed an unexpected behavior. Specifically, the `PASSIVE_UPDATE_V1` dispatch stood out. It accounted for over 30% of the gateway traffic, despite representing only about 2% of the total dispatches sent to clients. This discrepancy highlighted that `PASSIVE_UPDATE_V1` was responsible for a disproportionately large amount of data being transmitted.

Passive sessions are used to avoid sending most server-generated messages to clients who aren't actively viewing the server. For instance, even if a Discord server sends thousands of messages per minute, it wouldn’t make sense to waste bandwidth sending these messages to a user who isn’t reading them. Once the user views the server, the passive session upgrades to a normal session and starts receiving all dispatches.

However, passive sessions still need periodic updates to stay synced with the server. The `PASSIVE_UPDATE_V1` dispatch handles this by sending updates with lists of channels, members, and members in voice. The issue was that even if only one element changed, the entire list of channels or members was sent. While this approach worked when scaling Discord servers to hundreds of thousands of users, it became inefficient as the company continued to grow, leading to unnecessary bandwidth usage.

To address this, Discord introduced `PASSIVE_UPDATE_V2`, a new dispatch that only sends the changes (or delta) since the last update. This change drastically reduced the bandwidth usage for passive updates, cutting the gateway’s bandwidth from 35% to 5%, resulting in a 20% reduction in traffic across the entire cluster.

## Big Savings

Thanks to both the effects of Passive Sessions V2 and zstandard streaming, Discord was able reduce the gateway bandwidth usage of their clients by 40%.

Although optimizing passive sessions was an unintended side-effect of the zstandard experimentation, it highlights how effective instrumentation and a critical analysis of metrics can lead to significant improvements. By closely examining the data, the Discord team was able to achieve substantial savings with a relatively small investment of effort. This shows the value of carefully monitoring system performance and being open to unexpected opportunities for optimization.

## Sources

- <https://discord.com/blog/how-discord-reduced-websocket-traffic-by-40-percent?utm_source=newsletter.programmingdigest.net&utm_medium=newsletter&utm_campaign=how-discord-reduced-websocket-traffic-by-40&_bhlid=b66ab2f31c98310c457dceef10410fe3ea2d7125>
- <https://facebook.github.io/zstd/>
- <https://www.zlib.net>
- <https://github.com/silviucpp/ezstd>
- <https://logo.com/blog/the-history-of-the-discord-logo> (Cover Image)

[^1]: _gateway_ is the name of the service which provides a client with real-time updates
[^2]: zlib is a widely used multiplatform data compression library written in C. (<https://www.zlib.net>)
[^3]: _ezstd_ is an open-source binding of zstandard for the erlang language. (<https://github.com/silviucpp/ezstd>)