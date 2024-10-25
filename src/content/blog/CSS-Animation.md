---
title: CSS Animations
description: This article explores how to animate elements with dynamic heights in CSS using the max-height property. It provides practical examples, including a dropdown menu and an accordion, demonstrating how these techniques can enhance user interfaces with smooth transitions.
pubDate: 23 Oct, 2024
author: "de Rubinat Julien"
tags:
  - CSS
  - Animation
imgUrl: '../../assets/AnimationCSS.png'
layout: '../../layouts/BlogPost.astro'
---
# CSS Animations: Handling `height: auto` with `max-height`

## Introduction

Animating elements in CSS, particularly those with dynamic heights, has always been a challenge. The new CSS property simplifies this task, allowing smooth transitions without needing fixed heights. This article presents an explanation of this technique along with practical examples to illustrate its use.

## Explanation

Traditionally, animating elements with `height: auto` was tricky. Developers often used workarounds like `max-height` to set an upper limit on the height. This approach allows creating animations for elements such as dropdown menus or accordion panels. The key is to combine `max-height` with CSS transitions for fluid effects.

## Examples

### Example 1: Dropdown Menu

This code creates a dropdown menu whose height is animated when clicking the button.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Dropdown Menu</title>
    <style>
        .container {
            overflow: hidden;
            max-height: 0;
            transition: max-height 0.5s ease-out;
        }
        .active {
            max-height: 200px; /* Adjust based on content */
        }
        button {
            cursor: pointer;
        }
    </style>
</head>
<body>
    <button onclick="toggleMenu()">Toggle Menu</button>
    <div class="container" id="menu">
        <p>Item 1</p>
        <p>Item 2</p>
        <p>Item 3</p>
    </div>

    <script>
        function toggleMenu() {
            const menu = document.getElementById('menu');
            menu.classList.toggle('active');
        }
    </script>
</body>
</html>
```
### Example 2: Accordion Animation

This example demonstrates how to create an accordion with sections that unfold using CSS transitions.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Accordion</title>
    <style>
        .panel {
            overflow: hidden;
            max-height: 0;
            transition: max-height 0.5s ease-out;
            background: #f1f1f1;
            margin: 5px 0;
        }
        .active {
            max-height: 100px; /* Adjust based on content */
        }
        .accordion {
            cursor: pointer;
        }
    </style>
</head>
<body>
    <div class="accordion" onclick="togglePanel(this)">Section 1</div>
    <div class="panel" id="panel1">
        <p>Content of Section 1.</p>
    </div>
    <div class="accordion" onclick="togglePanel(this)">Section 2</div>
    <div class="panel" id="panel2">
        <p>Content of Section 2.</p>
    </div>

    <script>
        function togglePanel(element) {
            const panel = element.nextElementSibling;
            panel.classList.toggle('active');
        }
    </script>
</body>
</html>
```
## Conclusion
New CSS properties like max-height simplify the animation of elements with dynamic heights. By combining these properties with transitions, you can create more interactive and appealing user interfaces. The examples provided demonstrate how easy it is to integrate these techniques into your web projects.

## Source 
Kevin Powell. (2024, 16 octobre). This new CSS property just solved animating to height auto. https://www.youtube.com/watch?v=JN-nme9oF10