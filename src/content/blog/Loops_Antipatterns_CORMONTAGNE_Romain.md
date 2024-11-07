---
title: Antipatterns in Loops
pubDate: Nov 8, 2024 at 15h15
author: Cormontagne Romain
tags:
  - C#
  - Design Patterns
  - LINQ
imgUrl: '../../assets/antipatterns.jpg'
description: Loops can often be seen as antipatterns. You could be concerned, as they are a fundamental structure in most languages, but not all loops are antipattern. Learn here which ones, and what you can do to fix them
layout: '../../layouts/BlogPost.astro'
---
# Antipatterns in Loops

The main reason why antipatterns[^1] are found in code, is a lack of knowledge? It's also the cause of antipatterns in loops. Let's see how loops can contain antipatterns and be one.

_Note: in this article the code shown and the workarounds provided are written in C#_

## Replacing a Loop with a Functional Approach

Let's first examine a beginner-written loop aimed at calculating the total price of items excluding cakes, pointing out typical pitfalls and areas for improvement:

```cs
public static double CalculateTotalPrice(List<BakedGood> bakedGoods)
{
    double total = 0;
    foreach (BakedGood bakedGood in bakedGoods)
    {
        if (bakedGood is Cake)
        {
            continue;
        }
        total += bakedGood.Price;
    }
    return total;
}
```

Using a `foreach` loop with an `if` statement to exclude items can make code harder to read, as each line must be analyzed individually. In this pattern, the `if` statement is an exclusion with `continue`, meaning no action is taken for cakes, while a running total is managed outside the loop.

Using LINQ is a very good way to apply a functional approach to this loop, while being more readable and maintainable:

```cs
public static double CalculateTotalPrice(List<BakedGood> bakedGoods)
{
    return bakedGoods
        .Where(bakedGood => !(bakedGood is Cake))
        .Sum(bakedGood => bakedGood.Price);
}
```



In contrast, a LINQ approach is more concise and readable. The `Where()` filter clearly excludes items (indicated by `!`), and `Sum()` calculates the total in one line. The common antipattern to avoid is using `for ... if` or `foreach ... if` structures when LINQ or other filtering methods would be clearer and more efficient.

## Infinite Loops

Infinite loops are indeed another type of antipattern, and they mainly occur due to a lack of attention when writing them, like for instance when writing a `while (...)` loop and making an error in the escape clause.

Let's consider the following code sample, consisting in taking a bakery customer's order until they decide to stop:

```cs
bool keepAdding = true;
List<BakedGood> order = new List<BakedGood>();

while (keepAdding)
{
    // ... code to add baked good to the order ...
}
```

Now this is basically a `while(true)` loop, which is infinite unless we add a `break` statement inside, or unless you add an escape clause in the loop.

## Complex Loop Logic

Inserting a complex logic inside of a loop block is also considered as an antipattern. For instance, let's have a look at this code, trying to find the most expensive bread in our bakery:

```cs
Bread mostExpensiveBread = null;
double maxPrice = 0;

foreach (Bread bread in breadList)
{
    double discountedPrice = bread.Price;
    if (bread.IsOnSale)
    {
        discountedPrice *= 0.9; // 10% discount
    }

    if (CustomerLoyaltyProgramMember)
    {
        discountedPrice *= 0.95; // 5% loyalty discount
    }

    if (discountedPrice > maxPrice)
    {
        mostExpensiveBread = bread;
        maxPrice = discountedPrice;
    }
}
```

To fix this antipattern, we can just extract the discounted price calculation logic into its own function:

```cs
double CalculateDiscountedPrice(Bread bread)
{
    double discountedPrice = bread.Price;
    if (bread.IsOnSale)
    {
        discountedPrice *= 0.9; // 10% discount
    }

    if (CustomerLoyaltyProgramMember)
    {
        discountedPrice *= 0.95; // 5% loyalty discount
    }

    return discountedPrice;
}
```
and then call that function using LINQ instead of a loop:

```cs
var mostExpensiveBread = breadList
    .Select(bread => new { 
        Bread = bread, 
        DiscountedPrice = CalculateDiscountedPrice(bread) 
    })
    .OrderByDescending(x => x.DiscountedPrice)
    .FirstOrDefault()?.Bread;
```
By using LINQ as well as we can together with refactoring options, the code becomes more readable and easier to maintain.

Loops are often seen as antipattern because functional alternatives exist and the developer is often not aware of their existence. Here, in C#, LINQ is often an excellent functional replacement to loops.


## Sources

- <https://blog.nimblepros.com/blogs/antipatterns-in-loops/?utm_source=newsletter.csharpdigest.net&utm_medium=newsletter&utm_campaign=a-comparison-of-rust-s-borrow-checker-to-the-one-in-c&_bhlid=ab8dfc7e17122c3deecb47fffcd2ff1f8090680f>
- <https://deviq.com/antipatterns/antipatterns-overview>
- 

[^1]: The word **antipatterns** refers to design patterns applied in code or team practices which are thought to solve problems but actually introduce more than they solve. (https://deviq.com/antipatterns/antipatterns-overview)