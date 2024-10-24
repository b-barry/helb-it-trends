---
title: Directed Acyclic Graph
pubDate: 2024-10-24 21:30
author: "EL BOUCHTILI Imaddine"
tags:  
  - Blockchain
  - Crypto
  - DAG
imgUrl: '../../assets/dag_logo.png'
description: Explanation of Directed Acyclic Graphs (DAG), their structure, functionality, and comparison with blockchain.
layout: '../../layouts/BlogPost.astro'
---

## DAG (Directed Acyclic Graph)

### What is a DAG
A DAG is a graph-based data structure that represents a set of nodes (Vertices) and edges (Edges).

In a DAG, transactions validate previous transactions, acting as proof of correctness.

### How it works
A DAG consists of two important elements:

- **Vertices**: These represent the data in a DAG. Each vertex is a distinct entity, but two vertices can share associated properties or values.

- **Edges**: These are links between two vertices with a defined direction, meaning they are one-way paths.

> **Key Point : No loops !**

### Difference with Blockchain
While blockchain consists of a linear chain of blocks, a DAG is an acyclic graph.

In a DAG, each transaction typically validates two previous transactions, allowing **parallel validation**.

DAGs are therefore **more efficient** (in small infrastructures) and **less expensive**. There is no proof of work, meaning there are **no transaction fees** (or minimal ones).

However, DAGs can become less efficient when dealing with dense graphs due to the complexity of validating all connections.

> **This also makes DAGs more energy-efficient !**

Blockchain uses consensus mechanisms for security, while a DAG depends on the graph's topology and validation rules.

---
Source : [Coin Academy - Qu'est ce qu'un DAG](https://coinacademy.fr/academie/technologie-dag/)