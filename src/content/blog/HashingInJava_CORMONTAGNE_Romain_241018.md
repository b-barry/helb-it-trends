---
title: Exploring Hashing in Java
pubDate: Oct 18, 2024 at 15h15
author: Cormontagne Romain
tags:
  - Java
  - Hash
  - Collections
imgUrl: '../../assets/java-hashing-cover.jpeg'
description: HashSets, HashMaps, hashCode()... those are crucial for efficient data storage and retrieval in Java. Let's break down everything about them !
layout: '../../layouts/BlogPost.astro'
---
# Exploring Hashing in Java

Hashing converts data into a numeric value with a determined size known as _hash code_, which allows for fast searches, inserts, and deletions in data structures. It helps achieve fast data retrieval and prevents duplicates. In Java, hashing is ruled by three pillars : `HashSet`, `HashMap` and the `hashCode()` method.

## HashMap in Java

Firstly, here's a quick overview of the `Map` hierarchy in Java.
![Map Hierarchy in Java](https://media.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2F8pn079sof7pl37qjctij.png)

A HashMap stores data with key-value pairs, and uses the hash code of the key to quickly locate the corresponding value (hence the HashMap denomination). With a HashMap, searching for a value is pretty fast. Plus, it ensures that the keys are unique, and perfectly supports `null` values

The following executable Java Code shows basic operations offered by the `HashMap` class:
```java
import java.util.HashMap;

public class HashMapExample {
    public static void main(String[] args) {
        HashMap<Integer, String> userMap = new HashMap<>();

        // Inserting elements
        userMap.put(101, "Alice");
        userMap.put(102, "Bob");
        userMap.put(103, "Charlie");

        // Retrieving elements using their keys
        System.out.println("User with ID 101: " + userMap.get(101));

        // Removing elements based on keys
        userMap.remove(102);
        System.out.println("After removing ID 102: " + userMap);
    }
}
```

## HashSets in Java

A `HashSet` is a unordered collection of elements. It ensures that only unique elements are stored, using the `hashCode()` method to filter duplicates, which enables fast insertions and deletions.

Here's an overview of the `Set` class implementation in Java's structure (which is implemented by the `HashSet` class), and basic operations in the code that follows:
![](https://media.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fijd7qu3nezlj5svy0o0e.png)

```java
import java.util.HashSet;

public class HashSetExample {
    public static void main(String[] args) {
        HashSet<String> userSet = new HashSet<>();

        userSet.add("Alice");
        userSet.add("Bob");
        userSet.add("Charlie");
        userSet.add("Alice");
        // The same value is added twice, but the set won't store a duplicate ! Should also work with other reference types
        System.out.println("Is Bob in the set? " + userSet.contains("Bob"));

        userSet.remove("Charlie");

        System.out.println("Users in the set: " + userSet);
    }
}
```

## The `hashCode()` method

The `hashCode()` method originates from the super class `Object`, and can be overridden by any class we build. This method generates a unique code representing the data of an object. Whenever we try to store custom class objects in a `HashMap` or `HashSet`, overriding the `hashCode()` method together with the `equals()` method is essential to maintain an efficient storage and retrieval of the objects.

When an object is added to a `HashMap`/`HashSet`, the `hashCode()` of that object is firstly checked to determine its location, and then the `equals()` method is used to compare the objects properly.

## Best practices

It's always safer to override `hashCode()` and `equals()`. Note that if `equals()` returns that two objects are equal, they **must** share the same `hashCode()` value.

Depending on your level, you'll want to either grasping the use of hash codes in Java, systematically override those two functions, or explore hash collisions and performance optimization on larger scale applications.

## Sources

- https://dev.to/devnenyasha/understanding-hashing-in-java-exploring-hashmap-hashset-and-hashcode-2egh
- https://hackernoon.com/mastering-hashing-in-java-a-comprehensive-guide-to-hashmap-and-hashset (Cover Image)