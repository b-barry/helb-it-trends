---
title: GitGuardian Visual Studio Code Extension
pubDate: 2024-10-17 16:40
author: "EL BOUCHTILI Imaddine"
tags:  
  - GitHub
  - Visual Studio Code
  - GitGuardian
  - Extension
imgUrl: '../../assets/gitguardian_extension_logo.png'
description: How a new extension on visual studio code can help avoid secret leak on github page
layout: '../../layouts/BlogPost.astro'
---

## GitGuardian
[GitGuardian](https://www.gitguardian.com) is a platform designed to detect sensitive information (API keys, tokens, password, …) in source code in Git repositories. It works by scanning repositories, commits, and other activities.

I've already redacted an article on GitGuardian, [check it](https://helb-it-trends.beyondtime.io/blog/gitguardian/) before reading this article !

### Visual Studio Extension
A Visual Studio extension is an add-on that enhances the functionality of the Visual Studio IDE. These extensions can introduce new features or improve existing ones, such as :
- Code formatting
- Themes
- Tools

Extensions are available in the [Visual Studio Marketplace](https://marketplace.visualstudio.com/VSCode).

### GitGuardian Extension
The GitGuardian Visual Studio Code extension is a new tool that allows developers to scan their source code for exposed secrets and sensitive information before committing their changes. By integrating GitGuardian's security scanning directly into Visual Studio Code, this extension helps prevent secret leaks in real-time.

Once installed, the extension automatically scans your code for any credentials, API keys, or other sensitive data. If any secrets are detected, it alerts you immediately, allowing you to take corrective action before pushing the code to a remote repository. The extension can detect over 350 types of secrets, making it a powerful tool for improving security hygiene in development environments.

Key features of the GitGuardian VSCode extension include:

- Real-time scanning: It checks your code as you write and alerts you to potential secrets.
- Detailed security reports: Provides insights and suggestions on how to handle exposed secrets.
- Flexible configuration: Customize the scanning rules to fit the specific needs of your project.
- Seamless integration: Works alongside your Git workflow, catching sensitive data before commits or pull requests.

---
Source 1 : [Help Net Security - GitGuardian Visual Studio Code extension helps developers protect their sensitive information](https://www.helpnetsecurity.com/2024/10/14/gitguardian-visual-studio-code-extension/) 

Source 2 : [GitGuardian - VsCode extension](https://marketplace.visualstudio.com/items?itemName=gitguardian-secret-security.gitguardian)