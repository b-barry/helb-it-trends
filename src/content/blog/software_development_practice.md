---
title: Effective Software Development Practices
pubDate: Friday 8th november 2024
author: "Lenny SOLTAN"
tags:
  - SoftwareDevelopment
  - GoodPractices
imgUrl: '../../assets/software_development_practices.jpeg'
description: This article outlines practical habits that the author has found helpful in boosting development speed and quality.
layout: '../../layouts/BlogPost.astro'
---

# Effective Software Development Practices

This article outlines practical habits that the author has found helpful in boosting development speed and quality. These insights serve as personal guidelines for maintaining productive coding habits.

Source: [Effective Software Development Practices](https://zarar.dev/good-software-development-habits/)

## 1. Keep Commits Small

Small, manageable commits make tracking and reverting changes easier. Aim for commits that introduce minimal changes but still compile, avoiding merge conflicts and simplifying debugging.

## 2. Continuous Refactoring

Embrace Kent Beck’s advice: “for each desired change, make the change easy (which may be hard), then make the easy change.” Regularly refactor code in small increments to maintain a clean, adaptable codebase.

## 3. Focus on Working Software

Deploy frequently to ensure your code functions as intended in production. Tests provide confidence, but deploying confirms progress and functionality. Follow Agile principles: working software is the primary measure of progress.

## 4. Trust the Framework

Avoid testing the framework's functions (e.g., `useState` in React), as they are already well-tested. Smaller components reduce testing needs, as frameworks handle more functionality with less complexity.

## 5. Isolate Functions in New Modules

If a function doesn’t clearly belong in an existing module, create a new one. It’s better for maintainability than forcing it into an unrelated module, even if it remains isolated.

## 6. Use Tests to Define APIs

When unsure of an API’s design, start by writing tests, as this forces you to consider usability and edge cases. Test-Driven Development (TDD) helps clarify API expectations, even if you adapt TDD’s strictness for productivity.

## 7. Avoid Excessive Duplication

Duplicate code once, but if it occurs a third time, create an abstraction to manage it. This prevents divergent implementations and facilitates future improvements in one place.

## 8. Embrace Design Change

Designs age and often need rethinking. Accept that changing software is part of development. Refactor frequently to slow the rate of staleness, but be ready to overhaul designs as requirements evolve.

## 9. Manage Technical Debt Wisely

Classify technical debt by urgency: immediate blockers, potential future issues, and unlikely issues. Focus on the first two categories to minimize roadblocks and keep work progressing smoothly.

## 10. Prioritize Testable Design

Good design enables testability. If code is difficult to test, re-evaluate the design or use mockable abstractions to simplify testing, ensuring essential tests don’t go unwritten due to complexity.
