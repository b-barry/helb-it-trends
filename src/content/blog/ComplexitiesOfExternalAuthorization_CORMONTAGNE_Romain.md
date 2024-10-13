---
title: The technical complexities of external authorization
pubDate: Oct 11, 2024 at 15h15
author: Cormontagne Romain
tags:
  - Architecture
  - Good Practices
imgUrl: '../../assets/oauth-2.png'
description: Learning about the good and bad sides of external authorization
layout: '../../layouts/BlogPost.astro'
---

# The technical complexities of external authorization

Externalized authorization is the best way to go to keep authorization processes scalable, easy to maintain and to integrate with components, but those benefits are hard to obtain if the implementation of authorization is not planned well enough.

Practically, it can bring new challenges which are hard to notice. With this article, we will learn about strategies to dodge those traps, to ensure authorization gets implemented a correct way. But what is external authorization, exactly ? Before digging into that matter, let's learn about the basics.

Authorization is crucial to keep an application secure, since it determines the actions that a user has the right to do or not. However, the authorization processes become more complex as the applications grow, and it becomes even worse when the application involves microservices or distributed systems. The solution to this lies in external authorization. Now, let's see how it works, and the traps to watch out for.

## What is external authorization, and why using it ?

External authorization, as the name suggests it, refers to the separation of the authorization processes from the main code of the application. In monolithic applications,[^1] authorization is located inside the single codebase of the application, under classes or functions. Externalized authorization aims at transforming the related components into an independant service which interacts with the main code. The interface between them typically consists in calls to an API provided by the new authorization service.

This solution is often combined with external identity providers, meaning that the storage of user account data and role management comes under the responsibility of the used authentication platform. The application can then receive the context from that platform to use its own authorization layer and allow an action or not for a user.

Such a structure makes authorization process more easily testable and iterated over, while centralizing its implementation. This way, all services of the application will use the same policies. The best part of it ? It is completely reusable by any other services that might be developed, which isn't offered by an application which authorization logic is coupled with the rest of the code.

## Complexities of externalized authorization

Even though externalized authorization has advantages over monolithic authorization, it can increase the complexity of a project, as it adds another service to maintain and keep compatible with the other ones of the application. Let's dive into different kinds of complexity that we might face with external authorization

### Integration with main app/service

When externalizing authorization, what is typically a synchronous process can sometimes produce errors and become unreachable.

This implies that the authorization layer must be called several times if errors occur which could potentially not repeat, such as an inconsistent network connection. If too many tries lead to failures, then the user's request should be denied to avoid unexpectedly granting authorization.

### Management of user accounts and permissions

Even with an external authorization process, we should keep user accounts and permissions management in mind.

The used service should be able to store all the required data for users, along with a permissions model which supports groups and roles. Afterwards, the application must be able to maintain configure and maintain user attributes and role assignments.

If the management of user accounts is not planned sufficiently, problems might pop out when reintegrating the components into the application. The users' information should be centralized across all the different services, and be accessible through a reliable mechanism.

### Handling data filtering and pagination

When data gets filtered for a better rendering, the permissions of the user have an influence on the data that's being displayed.

To reach this result, the authorization policies should be opposed to each item from the requested resources, so that only those which the user has the right to interact with can be effectively returned, those rights depending on both the user who performed the request and the resource which results from that request.

The obvious problem with this occurs when handling large data collections. That problem also propagates to pagination mechanisms. If an item is removed from the result because it's been denied, a replacement must be inserted from the database to match the targeted page size.

This complexity can be addressed by planning the integration of queries with the authorization policies. It's also a good option to choose a provider which includes features such as query plans[^2] to directly retrieve authorized resources without further verification, and filter the queries when they're made instead of filtering the results.

### Maintaing security and privacy

As we add services to an application, the number of vulnerabilities which can be exploited increases. An externalized authorization service is part of those weaknesses.

Unlike traditional authorization models, externalized ones are more visible and more easily investigated by attackers if not properly protected. Keep in mind that logs from your network activity show the requests being sent and their matching response.

Authorization APIs can also leak data if not secure. Make sure that the service you use only responds to known and trusted applications via service-to-service calls. If you don't, users with malicious intentions or an attacker could extract sensitive data by directly calling the authorization API.

### Ensuring scalability and reliability

The authorization processes should be optimized, as they are involved in nearly all user interactions. As such, they must prove themselves extremely scalable and reliable. Otherwise, they'd become a bottleneck which would be a serious threat to your application performance.

The primary danger from this point of view is the latency which comes from exernalizing authorization. Your authorization should adapt to user activity to ensure the shortest waiting times even during peaks of acivity.

Authorization should also be failure resilient. At best, it should never go down, to ensure that users can login or user permission dependant functionalities anytime. To achieve this, authorization services should be deployed as duplicate instances, to obtain an architecture which can tolerate crashes coming from isolated instances.

## Implement externalized authorization the right way

In this section, we will learn about good practices for externalizing authorization for an application.

### Use industry-standard protocols and frameworks

Keep in mind that authorization is still in its first steps in terms of standardization, even if some standards such as OAuth2 have emerged and grow.

An effort is currently underway to define standards for the interaction between components playing parts in the authorization process, along with common practices and approaches regarding RBAC[^3], ABAC[^4] and PBAC[^5].

- RBAC is used when we need to assign permissions based on roles.
- ABAC comes in handy when permissions depend on a specific attribute of both the user and the resource
- PBAC is preferred in complex environments where access must be dynamically handled through a policy engine and a policy definition language, to define the rules and apply them.

### Favor prebuilt authorization platforms and services

It's hard to build an authorization service from scratch, as you're responsible for its maintenance and respect of the security norms. Choosing a dedicated platform offers all the advantages of externalized authorization without the complexity.

These systems are interacted with using their own public APIs, and offer a good user and authorization management using various policy models, while freeing you from building your own mechanisms for storing, assessing and requesting authorization logic.

### Seek specialized expertise and resources when building your own solutions

If, due to sensitivity or legacy compatibility requirements, you are force to develop your own authorization layer, make sure you don't build it on your own.

Exctract the essential requirements of the solution, and compare it with the reference architecture, or ask for an external review from a specialized audit or pen-testing team to make sure your system is properly secured, so you can focus on building business parts of your system.

Try looking for guidance from open-source authorization services/platforms for potential workarounds for the challenges you might face.

## Sources
- <https://www.cerbos.dev/blog/the-technical-complexities-of-externalized-authorization?utm_campaign=externalized_authorization&utm_source=bonobo_press_programming_digest&utm_medium=email&utm_content=&utm_term=&_bhlid=1f9d5738c36b6d7734f51610bdc1a02ad642ac7b>
- <https://www.geeksforgeeks.org/monolithic-application/>
- <https://www.cerbos.dev/blog/filtering-data-using-authorization-logic>
- <https://auth0.com/blog/oauth-2-best-practices-for-native-apps/> (Cover Image)

[^1]: Monolithic applications are applications (which can be large) where all the components are packed together and tightly coupled. Such applications offer a strong independance, but often lack flexibility. All the aspects of the code are located on a single code platform
    (Source: <https://www.geeksforgeeks.org/monolithic-application/>)

[^2]: From my understanding, a query plan is a structure close to a tree, which describe conditions to fulfill for data to be included in results
    (Source: <https://www.cerbos.dev/blog/filtering-data-using-authorization-logic>)

[^3]: Role Based Access Control
[^4]: Attribute Base Access Control
[^5]: Policy Based Access Control