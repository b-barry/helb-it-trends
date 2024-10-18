---
title: "VSCode: File Auto Save Settings"
pubDate: 06/10/2024 18:30
author: "Izla Bagci"
tags:
  - VSCode
  - Auto Save
  - Settings
imgUrl: 
- 'https://mcusercontent.com/ea228d7061e8bbfa8639666ad/images/c0867e3f-bc28-0206-b159-86a6bca4ef12.png'
- 'https://mcusercontent.com/ea228d7061e8bbfa8639666ad/images/17ce10c0-8120-8ab3-8758-9d0ca12251ce.png'
description: "A guide to using the auto-save feature in VSCode, with detailed settings."
layout: '../../layouts/BlogPost.astro'
---

# VSCode : File auto save settings


For a while now, VS Code has included the feature to auto save the work, but it's set to "off" by default, which means that you need to activate it manually.

You can go to the settings and auto save **onFocusChange**, this will save your work when it loses focus, for example, if you open another tab or editor, your file will be saved before. **OnWindowChange**, this one will also save when the focus is lost, but it will save all tabs, not only the current one.

VS Code proposes also **Auto Save delay**, which is going to save your file after the time in milliseconds that you provide it.

![](https://mcusercontent.com/ea228d7061e8bbfa8639666ad/images/c0867e3f-bc28-0206-b159-86a6bca4ef12.png)

These two features were already here for a long time.
Recently they added two more, which are : 
- **Auto Save When No Errors**
- **Auto Save Workspace Files Only**

![](https://mcusercontent.com/ea228d7061e8bbfa8639666ad/images/17ce10c0-8120-8ab3-8758-9d0ca12251ce.png)


These will allow you to avoid saving your files with errors.

There’s one last setting that comes turned on by default: Files > Refactoring: Auto Save. This option saves any files that are being refactored automatically. However, if you don’t want this feature, you can easily turn it off.







[Click here to read more](https://vscode.email/archives/issue-127/)


Written on 06/10/2024 by

Izla Bagci

