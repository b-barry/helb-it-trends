---
title: Confusing Abstraction with Indirection
pubDate: Nov 8, 2024 at 15h15
author: Cormontagne Romain
tags:
  - Software Engineering
imgUrl: '../../assets/abstraction-strength.jpg'
description: Sometimes, when trying to improve codebases or refactoring them, we face a heavy usage of abstraction, which is responsible for the slowness of the program. We'll try and explain what to be aware of about abstractions in this post.
layout: '../../layouts/BlogPost.astro'
---
# Confusing Abstraction with Indirection
---

When working with abstraction-heavy codebases, it’s common to find code that, while organized, ends up being a maze of layers which don't add real value. These extra layers make debugging difficult, slow performance down, and divert the CPU from solving the actual problem. Not all abstractions are equal. Many simply add unnecessary indirection.

## What Makes a Good Abstraction ?

A good abstraction, like TCP, hides underlying complexity, allowing developers to work as if the details don’t exist. TCP handles error correction, retransmission, and sequencing so well that developers rarely need to dig into the lower-level details. This is the proof you're facing a great abstraction: it hides complexity effectively.

## The Darker Side of Abstraction

On the other hand, bad abstractions are layers of indirection, at best. They add no real functionality, only an extra level that makes tracing and understanding code harder. Such layers increase cognitive overhead without delivering on promises of flexibility or modularity, making codebases more complex and harder to optimize or debug.

## What do Abstractions Actually Cost ?

Abstractions coeme with real costs, in complexity and often in performance. Each new layer puts the code further from the core logic, adding mental and computational hurdles. This conflicts with both simplicity and maintainability, as each abstraction introduces its own rules and potential points of failure. Good abstractions minimize these issues, while bad ones make systems harder to maintain.

## All Abstractions Leak

A saying claims that "All abstractions eventually leak", and it's true. In some situations, it becomes necessary to understand the underlying details and the complexity of an abstraction. A useful test of an abstraction’s quality is to ask: how often do I need to look beneath it ? The less frequently this is needed, the stronger the abstraction.

## The Asymmetry of the Costs

Abstraction costs are also 'asymmetrical'. The creator of an abstraction gains immediate benefits in terms of cleanliness, flexibility, elegance and extension of the code, but others who maintain, debug, or optimize it later pay the price. These future developers are often the ones who deal with the additional complexity or performance issues.

## Conclusion

In conclusion, abstractions are valuable but costly tools. Good abstractions hide complexity, and bad ones just increases it. The next time you consider using an abstraction, ask yourself if it genuinely simplifies the system or just adds another layer. Use abstractions with care, focusing on truly hiding complexity rather than layering it on.

## Sources

- <https://fhur.me/posts/2024/thats-not-an-abstraction?_bhlid=3c79cbef249ab3fc6fc5f93ac2b046bacf96ccdb&utm_source=newsletter.programmingdigest.net&utm_medium=newsletter&utm_campaign=that-s-not-an-abstraction>
- <https://functionallyimperative.com/p/the-bigger-the-interface-the-weaker> (Cover Image)