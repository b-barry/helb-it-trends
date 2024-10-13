---
title: "Functions VS Generators : what to use in data science ?"
pubDate: 2024-10-11 15:15
author: Cormontagne Romain
tags:
  - Python
  - Data Science
  - Best Practices
imgUrl: '../../assets/generator-python.png'
description: A quick discovery of generators and their application in Python. Learning about their use cases and when to prefer them over normal functions
layout: '../../layouts/BlogPost.astro'
---

# Functions VS Generators : what to use in data science ?
When writing code in general, we may often face situations where we have to manipulate large volumes of data. In those situations, ensuring that the execution of the treatment script won't use too many resources nor take too much time is very important. In Python data science, **functions** and **generators** are two powerful tools to treat data, but since they behave differently, mastering their differences to make the best use of both of them is crucial to deliver optimized code.

## Functions
We all know what a function is, from a programming point of view. As a kind reminder, and to keep it simple, a function is block of instructions that's executed only when it is called. It can be passed parameters and return data as a result.

In Python, functions are declared following this structure :
```py
def foo(args):
    # Do some stuff
    return ... # The data returned by the function (optional)
```

## Generators
Generators are very similar to functions. They have a nearly identical structure inside code and, just like functions, they are executed only when called. The only difference with 'standard' functions lies in the way they return data. Unlike functions, generators use the `yield` keyword to return data. To say it another way, if a function returns data using `yield` as data returning statement, it automatically becomes a generator.

Typically, Python generators return iterable objects, meaning we can iterate on them using `for` loops. They can also be declared as expressions rather than as functions, using the _list comprehension_ technique. List comprehension is a technique that allows us to build a list using the algorithm that, if applied, would return the desired data, without having to write a full code block and allowing us to manipulate undetermined volumes of data directly in the definition of a list.

Here's a quick example. Let's say we want to make a list of all the even numbers between 0 and 10. The definition of the list would be the following :
```py
even_numbers = [ i for i in range(11) if i % 2 == 0 ]
print(even_numbers) # prints [0, 2, 4, 6, 8, 10]
```

Generator expressions work exactly the same way as list comprehension expressions. To distinct them from list comprehension, though, they are written with parentheses instead of brackets, resulting in the following :
```py
generator_exp = ( i for i in range(11) if i % 2 == 0 )

# We need to iterate over the generator to print data !
for i in generator_exp:
    print(i)
```

## Functions VS Generators : the underlying differences

When it comes to their deeper principles, functions and generators are much different. Using analogies, I will explain how different they are.

### Functions seen as a vending machine

Functions can be compared to vending machines. We pay some money, choose our product, and the machine delivers the item we ordered. The machine can be used multiple times, and it contains all the logic to release items based on the user input, immediately after receiving it. The following schema illustrates that situation pretty well :

![Functions and Vending Machine analogy](https://i0.wp.com/codecut.ai/wp-content/uploads/2024/10/2024-10-07_15-50.png?w=629&ssl=1)

To sum it up, the result is given as quickly and directly as possible, and the entirety of the data handled by the machine is processed before returning anything. This can be repeated as many times as we want.

Here's a code sample for such a machine :
```py
def vending_machine(money, selection):
    articles = { 
        "A1": { "name": "Chips", "price": 1.00 },
        "B2": { "name": "Chocolate", "price": 1.50 },
        "C3": { "name": "Soda", "price": 1.80 },
    }
    if selection in items and money >= articles[selection]['price']:
        return f"Here's your {articles[selection]['name']}. Enjoy !"
    return "Invalid selection or insufficient funds."

result = vending_machine(2.00, "B2")
print(result) # prints "Here's your Chocolate. Enjoy !"
```

### Generators seen as a bookmarked novel

Here, we compare generators with a long novel, a novel that we'd take quite a long time to read. We progress in the book only when needed, with bookmarks keeping track of the advancement and allowing resuming whenever needed. By doing so, the book isn't to be memorized entirely only the current page, but we cannot go backwards through the pages.

To illustrate this example, the following schema can be useful :

![Bookmarked novel generator illustrated](https://i0.wp.com/codecut.ai/wp-content/uploads/2024/10/2024-10-07_15-50_1.png?w=480&ssl=1)

And again, it can be represented by a very simple code :
```py
def bookmarked_novel():
    yield "Chapter 1"
    yield "Chapter 2"
    #...
    yield "Final Chapter"

story = bookmarked_novel()
print(next(story)) # Chapter 1
print(next(story)) # Chapter 2
```

To sum it up, to go through the whole dataset returned by the generator, it is necessary to call it several times, and after each call, progress is made based on the last returned data. Plus, it is impossible to reach data that's been returned previously.

## Use cases in Data Science

In Data Science, the choice between functions and generators will depend on the task which has to be performed.

- Functions will be used when we need to perform specific and repeatable tasks, like for example :
  - Cleaning, normalizing or encoding data
  - Create or update new features
  - Simplify the implementation of processes which assess the performance of a data model
- Generators are useful to handle very large datasets or code instruction sets which a resource consuming.
  - It can free the memory from being charged with a whole dataset and process it in chunks instead

## Conclusion : Choosing the right tool

Functions should be preferred to contain operations which can be quickly executed and repeated multiple times
Generators are to be used to handle large sets/streams of data. This way, the data can be processed incrementally, sparing some memory and allowing 'real-time' analysis

## Sources
- <https://codecut.ai/python-functions-and-generators-essential-tools-for-data-scientists/?link=button&utm_source=Klaviyo&utm_medium=email&utm_campaign=Wednesday%20Campaign&_kx=vuv_ZGxhDsLN4zv5aaMnt9zX1jqN9L4ssBDR03B6FCE.SgpyU4>
- <https://www.geeksforgeeks.org/generators-in-python/>
- <https://www.w3schools.com/python/python_functions.asp>
- <https://geekpython.in/python-generators-with-yield-statement> (Cover Image)