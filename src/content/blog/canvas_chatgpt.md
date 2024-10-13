---
title: Canvas Mode In ChatGPT 
pubDate: 2024-10-10 21:30  
author: "EL BOUCHTILI Imaddine"  
tags:  
  - ChatGPT
  - IA
imgUrl: '../../assets/chatgpt_logo.png'  
description: A new dev changing functionnality appear on ChatGPT.  
layout: '../../layouts/BlogPost.astro'  
---

## Canvas Mode In ChatGPT

### Introduction

The famous LLM ChatGPT has recently introduced a new feature for developers. To access it, you need to be a premium member of ChatGPT and ask ChaptGPT to activate it.

### Functionnality

This new mode allows developers to work even more efficiently with ChatGPT. It enables direct modification of outputs within a new interface. In this way, you can select a portion of the code and directly request a modification of a feature through the output.

For example, here is a code in C that adds and subtracts numbers :

```c
#include <stdio.h>

// Function to add two numbers
int addition(int a, int b) {
    return a + b;
}

// Function to subtract two numbers
int subtraction(int a, int b) {
    return a - b;
}

int main() {
    int x = 8;
    int y = 3;
    
    int sum = addition(x, y);
    int difference = subtraction(x, y);
    
    printf("The sum of %d and %d is %d\n", x, y, sum);
    printf("The difference between %d and %d is %d\n", x, y, difference);
    
    return 0;
}
```

Thanks to the new feature, if I want to modify the function that adds two numbers by adding a print statement inside it, I can simply select that section of code and, by adding a prompt, ChatGPT will understand that only the selected part should be modified.

Source : [OpenAI - ChatGPT Canvas](https://openai.com/index/introducing-canvas/)