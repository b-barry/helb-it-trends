---
title: Comment your code ! 
description: A good code should have good comments and good comments should help you to understand a code...
pubDate: 2024-11-02 18:24
author: "Friedrich Nihat Röben"
tags:
  - Code 
  - Comments
  - Contribution
imgUrl: '../../assets/code.webp'
layout: '../../layouts/BlogPost.astro'
---

## Comment your code !

A good code should have good comments and good comments should help you to understand a code...

---

### Introduction

Some people think that a good code don't need comments because the code itself will be the documentation. This is 
a mistake because not all comments explain the code but instead they explain what you can't understand from the code. 
Comments also help the reader as they can be a tool for lowering the amount of lecture.

### Function comments

Function comments serve a crucial purpose in programming: they are designed to prevent readers from needing to dive into 
the actual code. By placing these comments at the top of function definitions (they can also appear above classes, ...) 
they allow developers to treat the code as a "black box" with defined rules.
If the function comment is good, the user should be able most of the times to jump back to what he was reading without 
having to read the implementation of a function, a class or whatever.   

```bash
/* Calculate the factorial of a number. Returns -1 if number is negative,
 * otherwise returns the factorial value. This is a recursive implementation. */
int factorial(int n) {
    if (n < 0) return -1;
    if (n <= 1) return 1;
    return n * factorial(n - 1);
}
```

### Design Comments

Design comments are often placed at the begin of a file. They explain why and how a given piece of code uses a 
certain algorithm. It is a high-level overview of the code and it will help you reading it afterward. 

```bash
/* The design is trivial, we have a structure representing a job to perform
* and a different thread and job queue for every job type.
* Every thread waits for new jobs in its queue, and process every job
* sequentially. */

```

### Why comments

These comments explain why the code is doing something, even if it is clear why.

```bash
for (j = 0; j < dbs_per_call && timelimit_exit == 0; j++) {
    int expired;
    redisDb *db = server.db+(current_db % server.dbnum);

    /* Increment the DB now so we are sure if we run out of time
     * in the current DB we'll restart from the next. This allows to
     * distribute the time evenly across DBs. */

    current_db++;
```

### Teacher comments

Teacher comments serve a different purpose than regular code comments. Instead of explaining the code's mechanics 
or potential issues, they focus on educating the reader about the domain knowledge needed to understand the code. 
These comments help bridge knowledge gaps when readers encounter code that deals with specialized areas like mathematics, 
networking, statistics,...

```bash
/* Draw a square centered at the specified x,y coordinates, with the specified
 * rotation angle and size. In order to write a rotated square, we use the
 * trivial fact that the parametric equation:
 *
 *  x = sin(k)
 *  y = cos(k)
 *
 * Describes a circle for values going from 0 to 2*PI. So basically if we start
 * at 45 degrees, that is k = PI/4, with the first point, and then we find
 * the other three points incrementing K by PI/2 (90 degrees), we'll have the
 * points of the square. In order to rotate the square, we just start with
 * k = PI/4 + rotation_angle, and we are done.
 *
 * Of course the vanilla equations above will describe the square inside a
 * circle of radius 1, so in order to draw larger squares we'll have to
 * multiply the obtained coordinates, and then translate them. However this
 * is much simpler than implementing the abstract concept of 2D shape and then
 * performing the rotation/translation transformation, so for LOLWUT it's
 * a good approach. */
```

### Checklist comments

In a perfect world this type of comments should never been needed but the reality is different. Sometimes in coding, 
you can't put all related things in one place. This might be due to: language limits, design choices, system complexity,...
When this happens, you need comments to remind yourself (or others) to make changes in different parts of the code.

```bash
/* Warning: if you add a type ID here, make sure to modify the
 * function getTypeNameByID() as well. */
```

### Guide comments

Most of people think that guide comments are useless because they don't state what is not clear from the code, 
neither give they design hints. They just assist processing what is written in the code by providing rythm. 
They are usefull because they reduce the cognitive load of the programmer reading some code.

```bash
/* Check if buffer is full before adding new element.
 * Return -1 if full, 0 on success. */
if (buffer->size >= MAX_SIZE)
    return -1;
buffer->data[buffer->size++] = element;
return 0;

```

### Trivial comments

The last 3 types of comments are comments that you would avoid. If a guide comment is bad written it can become 
a trivial comment. This means that with this comment the cognitive load is not reduced but stays the same or is higher.

```bash
array_len++;	
/* Increment the length of our array. */
```

### Debt comments 

Debt comments are technical debts statements written inside the source code. FIXME, TODO, XXX, ...
are debt comments. They are not great in general, try to avoid them if possible because they is a big chance 
that you will forget them.

```bash
array_len++;	
/* Here we should perform garbage collection in case at this point
 * there are too many entries deleted inside the listpack. */
 entries -= to_delete;
 marked_deleted += to_delete;
 if (entries + marked_deleted > 10 && marked_deleted > entries/2) {
 /* TODO: perform a garbage collection. */
 }
```

### Backup comments

Backup comments are notes where the developer leaves the old version off the code in case the new version doesn't work.
This is a bad habit as nowadays you can just use git and see your older versions if needed.

```bash
array_len++;	
// Ancienne version, simple concaténation
// for (String name : names) {
//     result += name + ", ";
// }

StringBuilder result = new StringBuilder();  // Nouvelle version avec StringBuilder pour améliorer la performance
for (String name : names) {
    if (!name.isEmpty()) {  // ajout d'une condition pour ignorer les noms vides
        result.append(name).append(", ");
    }
}
```

### Conclusion

In conclusion, effective comments are essential to writing good, maintainable code. They clarify complex logic, 
explain design decisions, and help others (or even our future selves) understand why certain choices were made. 
While some comments, like backup comments, can be avoided through version control tools like Git, well-placed 
comments make the code clearer and more accessible. Remember: comments should add value, not clutter.

---

Source : http://antirez.com/news/124?_bhlid=d062cbcb66e407a98b7dc19bf547bde586fb2d06&utm_source=newsletter.programmingdigest.net&utm_medium=newsletter&utm_campaign=that-s-not-an-abstraction





