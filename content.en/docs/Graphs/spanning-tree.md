---
title: Spanning Tree
weight: 6
---

A **spanning tree** of a graph is an undirected tree consisting of only those edges that are necessary to connect all the vertices in the original graph.

**Properties:**
- For any pair of vertices, there exists only one path between them
- Insertion of any edge to a spanning tree forms a unique cycle

**Types:**
- **Depth First Spanning Tree:** Resulting from DFS
- **Breadth First Spanning Tree:** Resulting from BFS

**Applications:** Analysis of electrical circuits, shortest route problems, designing hydraulic/road/cable/computer networks

### Minimum Cost Spanning Tree

A graph may have weights on its edges. The **cost of a spanning tree** is the sum of costs of the edges in that tree. A **minimum cost spanning tree** has cost less than or equal to cost of all other spanning trees.

---

### Kruskal's Algorithm

In this algorithm, a minimum cost spanning tree T is built edge by edge:
- Edges are considered for inclusion in T in **increasing order of their costs**
- An edge is included in T if it **does not form a cycle** with edges already in T

**Example Process:**
1. Insert edge 4-3 (cost 1) - Include
2. Insert edge 4-2 (cost 2) - Include
3. Insert edge 3-2 (cost 3) - **Reject** (forms cycle 2-3-4)
4. Insert edge 4-1 (cost 4) - Include

**Minimum Cost:** 1 + 2 + 4 = **7**

---

### Prim's Algorithm

Steps involved:
1. Choose any vertex
2. Add it to the spanning tree vertex set and remove it from graph vertices set
3. Identify the vertices connected with the chosen vertex
4. Compare the weights of edges connecting the chosen vertex and identified vertices
5. Choose connected edge which has minimum weight
6. Add it to the spanning tree vertex set

**Constraint:** Do not choose a vertex already in the spanning tree vertex set or if it forms a cycle.

---