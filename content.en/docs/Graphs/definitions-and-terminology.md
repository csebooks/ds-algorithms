---
title: Definitions and Terminology
weight: 2
---

A graph consists of two sets **v** and **e**, where:
- **v** is a finite, non-empty set of **vertices**
- **e** is a set of pairs of vertices called **edges**

A Graph can be of two types:

### Undirected Graph
- The pair of vertices representing any edge is unordered
- Thus, the pairs (v1, v2) and (v2, v1) represent the same edge

### Directed Graph (Digraph)
- Each edge is represented by a directed pair `<v1, v2>`
- **v1** is the **tail** and **v2** is the **head** of the edge
- Therefore, `<v2, v1>` and `<v1, v2>` represent two different edges

> **Note:** The edges of a directed graph are drawn with an arrow from the tail to the head.

**Example:**
- **G1** (Undirected): Vertices = {1, 2, 3, 4}, Edges = {(1,2), (1,3), (1,4), (2,3), (2,4), (3,4)}
- **G2** (Directed): Vertices = {1, 2, 3}, Edges = {<1,2>, <2,1>, <2,3>}

---