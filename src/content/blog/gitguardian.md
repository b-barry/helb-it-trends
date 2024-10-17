---
title: GitGuardian
pubDate: 2024-10-10 22:30  
author: "EL BOUCHTILI Imaddine"  
tags:  
  - Git
  - Github
  - GitGuardian
imgUrl: '../../assets/gitguardian_logo.jpg'  
description: In this blog, you will know what is GitGuardian and how it work.  
layout: '../../layouts/BlogPost.astro'  
---

## GitGuardian

### Introduction

GitGuardian is a platform designed to detect sensitive information (API keys, tokens, password, ...) in source code in Git repositories. It works by scanning repositories, commits, and other activities.

### How GitGuardian Works

GitGuardian functions through continuous monitoring and integration with Git repositories. It employs specific and generic detectors to identify different types of secrets in private and public repositories. The platform provides alerts and remediation actions if sensitive information is detected, allowing devs to secure their repository.

### Secrets Detection Engine

The secrets detection engine uses a range of specific and generic detectors.

#### 1. Specific detectors

Specific detectors are built for known types of secrets (e.g., AWS keys, Google Cloud credentials).

```java
public static void useApiKey() {
    String apiKey = "AKIAEXAMPLE1234567890";

    // some stuff here
}
```

In this case, GitGuardian’s would identify the API key format and alert the repository owner.

#### 2. Generic detectors

Generic detectors identify unknown or custom secrets by analyzing patterns.

```java
public static void connectToDatabase() {
    String dbUrl = "127.0.0.1/users";
    String username = "admin";
    String password = "SuperSecret1234Password!";

    // some stuff here
}
```

In this scenario, GitGuardian's generic detector might flag the password based on its length and pattern, alerting the repository owner of the potential security risk.

If GitGuardian detects any secrets in the code, it will notify the owner with recommended solutions for remediation, such as removing the secrets from the code and commit history.

---

Source 1 : [GitGuardian - How it work](https://openai.com/index/introducing-canvas/)

Source 2 : [GitGuardian - Specific vs generic detectors](https://docs.gitguardian.com/secrets-detection/secrets-detection-engine/detectors/introduction)