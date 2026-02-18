---
title: Graph Representations
weight: 4
---

There are three commonly used representations for graphs:

### (a) Adjacency Matrix

An adjacency matrix of a graph is a 2-dimensional array of size **n × n** (where n is the number of vertices) with the property that:
- `a[i][j] = 1` if the edge (vi, vj) is in the set of edges
- `a[i][j] = 0` if there is no such edge

**Properties:**
- The adjacency matrix for an **undirected graph is symmetric**
- The adjacency matrix for a **directed graph need not be symmetric**
- Space needed: **n² locations**
- For undirected graphs, about half the space can be saved by storing only the upper or lower triangle

### (b) Adjacency Lists

This is a **vertex-based representation**. In this representation:
- An array is used to store the vertices
- Each array element contains the vertex label, any other related information, plus a pointer to a linked list of nodes containing adjacent vertices
- The array provides random access to the adjacency list for any particular vertex

**Advantage:** We can quickly find all edges associated with a given vertex by traversing the list, instead of having to look through possibly hundreds of zero values in an adjacency matrix.

**Note:** For an undirected graph, each edge-information appears twice.

### (c) Adjacency Multi-lists

An adjacency multi-list is an **edge-based representation** rather than vertex-based. Each node that represents an edge consists of 5 fields:

| Flag | Vi | Vj | Next link for Vi | Next link for Vj |

- Like adjacency list, an array of vertices is maintained
- Each array element points to a suitable edge node

**For directed graphs:** There would be two elements for each vertex in the array—one when the vertex is head of an edge and another when it is a tail.

---