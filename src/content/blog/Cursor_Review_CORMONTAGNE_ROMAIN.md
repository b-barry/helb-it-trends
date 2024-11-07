---
title: A Review of the LLM Powered Coding Tool 'Cursor'
pubDate: Nov 8, 2024 at 15h15
author: Cormontagne Romain
tags:
  - IDEs
  - LLMs
imgUrl: '../../assets/cursor-editor.png'
description: AI is being added to our IDEs very quickly nowadays. However, not all these tools behave the same way. Cursor is one of them. And we will show you if it is worth buying its subscription or not.
layout: '../../layouts/BlogPost.astro'
---
# A Review of the LLM Powered Coding Tool 'Cursor'
---
Cursor[^1] is a fork of Visual Studio Code that incorporates Large Language Model (LLM) features directly into its core user interface. However, even though it can be used for free or through a paid subscription, the advantages of that subscription are quite blurry. We'll try and understand those better by examining the features of the tool.

Among those features, we find :
- **Tab Completion** : (_Exclusive to subscribers_) This feature uses fine-tuned models to provide code completion and navigation between different recommended actions, all triggered by the _Tab_ key.
- **Inline Editing** : This is a chat-based interface which allows for easy code edits with a simple diff[^2] view, powered by models like GPT or Claude.
- **Chat Sidebar** : This is a sidebar view for large edits, enabling discussions, multi-file code suggestions and more, also leveraging GPT or Claude.
- **Composer** : Designed for larger cross-codebas, _Composer_ allows user to generate and approve diffs accross mutliple files in a chat-based interface.

Let's get more into the details of those features.

## Tab Completion

_Tab Completion_ stands out as the most intuitive and time-saving tool for coding. Unlike other LLM-powered tools which are more based on chat interactions, _Tab Completion_ integrates well into coding workflows. It's highly refined, and can suggest completions for single lines but also recommend a logically suiting next line for further edits. In practice, you only need to start a change on a line and then use the _Tab_ key to auto-complete related updates across your entire file, which significantly boosts productivity.

It can also be used as a powerful code refactoring tool to automate tasks in which errors get easily inserted without needing to write custom scripts. For example, if you have a block of code written into snake_case which you'd like to convert into camelCase, you can simply rename one instance of a variable and let _Tab Completion_ do the rest for you by continuously pressing the _Tab_ key. This is a very effective way of streamlining the refactoring process.

Oftentimes, _Tab Completion_ will find and fix bugs. For instance, if your code contains an issue, the feature might identify it and propose a potential fix. It's also able to suggest imports when adding a dependency in languages like Python or Go. Another example is when you work with strings. When you wrap a string with quotes, the contents will be automatically escaped, ensuring proper syntax. Furthermore, Cursor can generate entire functions based just on its signature and an optional docstring.

Overall, Cursor feels like it’s anticipating your next move. It enables the devs to focus less on the mechanics of writing code and more on the architecture of their project.

Another standout feature of Cursor is how fast the completions are. The suggestions appear almost immediately after stopping typing. This responsiveness is crucial, as any significant lag would disrupt the flow of coding and hinder productivity. This generation speed ensures a seamless and efficient coding experience.

One minor downside of _Tab completion_ feature is that sometimes the suggestions don’t appear in time, especially when typing quickly. It won't show up if you continue typing before it appears, and once that happens, there doesn’t seem to be a way to bring it back. This can sometimes force you to type something else and hope that the correct suggestion reappears, which can be a bit frustrating.

Another disadvantage is the opposite issue: sometimes a suggestion is completely wrong, which must then be dismissed. However, on rare occasions, upon accepting a totally different completion, the previously declined suggestion gets applied quietly in the background. This can cause sttealthy bugs because you don't get to knwo that the wrong logic had been accepted. While these cases don’t happen often enough to outweigh the overall productivity boost of Tab completion, they do detract from the tool’s reliability and can introduce some confusion during development.

## Inline editing, chat sidebar, and composer

All of these features seem to work similarly by interacting with a foundational model. The main difference between them appears to be in the user interface rather than the underlying functionality.

_Inline editing_ in Cursor is triggered by selecting some code and pressing **Ctrl-K** (or **Cmd-K** on macOS). Once invoked, the desired changes can be typed in, and it generates a diff within the file. This feature is primarily used for implementing small code snippets within a function or for minor refactoring tasks, as it provides an easy and efficient way to make changes while visually seeing the differences. It works especially well when you want to parallelize tasks from a loop.

The _Chat Sidebar_ in Cursor is opened with **Ctrl+L** (or **Cmd+L** on macOS), providing more screen space for a multi-turn conversation. A minor flaw of the LLMs it integrates is that they often return code first, without asking for clarification when there’s ambiguity in the request. However, the chat sidebar itself is quite handy for handling larger tasks. The suggested code within the sidebar has an _Apply_ button, which generates a diff in the currently selected file. This feature is particularly useful for larger refactors within a single file or when creating an entirely new file based on the one you have open. If other files are relevant, they can be added manually, but Cursor will also try to automatically detect the relevant files based on the query and its background index, streamlining the process even further.

_Composer_ is designed specifically for cross-file refactors, allowing for larger, multi-file changes to be handled efficiently. While this feature is the least used one, it offers a better user experience when reviewing multiple file diffs one at a time. _Composer_ allows you to generate diffs for changes across different files, and you can page through and approve them sequentially. This makes it easier to manage significant refactoring tasks that span multiple files without getting overwhelmed by the changes.

## The `.cursorrules` file

Cursor’s various chat modalities include the contents of a `.cursorrules` file located at the workspace root, which provides additional context to the LLM. The documentation is unfortunately minimal on this feature, so it needs some exploring to learn more about it. This file can be used to inform the LLM of coding standards, common packages, and other project-specific documentation. This proves helpful in tailoring suggestions and maintaining consistency with the repository’s practices.

A well-structured `.cursorrules` file can indeed be a valuable way to guide the LLM in using project-specific libraries and coding patterns consistently. By defining the use of your proprietary context-passing library in `.cursorrules`, you might help the LLM recognize and apply these practices even when they’re not present in the file being edited, making it easier to maintain consistency across the codebase.

A current limitation with the `.cursorrules` feature is that it only supports one file per workspace, which makes it harder to configure for monorepos like yours with multiple languages. Setting up coding standards and patterns becomes simpler in smaller repositories with consistent styles, but accommodating diverse codebases in a monorepo would likely require more nuanced rules or workarounds to capture the unique needs of each language and sub-project.

Cursor’s `.cursorrules` file is officially designed to provide additional context to LLMs during chat-based interactions. While it’s intended solely for chat modalities, pinning the `.cursorrules` file as an open tab in the workspace can extend its influence to tab completion, offering a useful workaround for applying consistent practices across different coding modes in Cursor.

## Changes in the workflow

The real appeal of Cursor lies not in merely speeding up code writing — since typing itself is rarely the main bottleneck — but in transforming the way you approach coding. By streamlining repetitive tasks, Cursor allows programmers to focus less on individual lines of code and more on the high-level problem at hand. This shift in workflow promotes a more strategic, solution-oriented approach to development.

These are the aspects of your work that can change with Cursor and LLMs :

1. **Reduced Dependency on Libraries**: You should become less inclined to pull in external libraries for small utilities, instead having the LLM create custom solutions tailored for your project, where general-purpose libraries would bring extra overhead and dependencies which can complicate maintenance over time.
2. **Shift in _DRY_ Principles**: The ability to quickly generate repetitive code makes you less strict about _**DRY**_ (**Don't Repeat Yourself**) in early development stages. However, avoiding premature abstractions allows flexibility, and it's always possible to refactor with the LLM’s help if needed.
3. **Increased Comfort with New Languages**: With the LLM assisting, enthusiasm towards unfamiliar languages grows faster, as you can get the right code quickly, making tasks that once took hours possible in minutes.
4. **Prototyping in Isolation**: You can prototype smaller components in one language, work out the details, and then transfer them to another language or a more robust setup, such as integrating Python logic into a Go-based web app. The LLM aids in generating test data, mocks, and other scaffolding, making it easier to iterate without dealing with the complexities of a mature codebase.

## Conclusion

Currently, Cursor is one of the best examples of the potentials of LLM coding assistants, and you can always give it a try if you want to explore how this type of tool might be of value to you and your projects !

## Sources

- <https://www.arguingwithalgorithms.com/posts/cursor-review.html?utm_source=newsletter.programmingdigest.net&utm_medium=newsletter&utm_campaign=the-weirdest-timezone&_bhlid=39770e32d9575385703617a9301a7a1152ef9c63>
- <https://medium.com/@mayurkoshti12/cursor-ide-an-ai-powered-code-editor-7129d26bee5f> (Cover Image)

[^1]: See [Cursor](https://cursor.sh/)
[^2]: A diff view is a file comparison interface highlighting the differences between two version of a same file