---
title: 'Graphs'
weight: 8
references:
    books:
        - b1:
            title: Data Structures and Algorithm Analysis in C by Mark Allen Weiss 
            url: https://mrajacse.files.wordpress.com/2012/08/data-structures-and-algorithm-analysis-in-c-mark-allen-weiss.pdf
        - b2:
            title: Data_Structures_and_Algorithm_Analysis_2e By mark-allen-weiss
            url: https://www.google.co.in/books/edition/Data_Structures_and_Algorithm_Analysis_i/83RWbPynhkgC?hl=en&gbpv=1

---

# Chapter 8: Graphs
## Spread Your Tentacles

### Why This Chapter Matters!
Networking! Be it any walk of life, that's the keyword today. Better your network, farther you would reach, and farther you spread your tentacles, better would be your network. And the crux of building and managing a network is hidden in a subject as innocuous as data structures in a topic called Graphs. Naturally, you must learn it to the best of your ability.

---

## Definitions and Terminology

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

## Adjacent Vertices and Incident Edges

### Undirected Graph
- If (v1, v2) is an edge, then vertices v1 and v2 are said to be **adjacent**
- The edge (v1, v2) is **incident** on vertices v1 and v2

**Example:** In G1, vertex 2 is adjacent to vertices 1, 3, and 4. The edges incident on vertex 3 are (1,3), (2,3), and (4,3).

### Directed Graph
- If `<v1, v2>` is a directed edge, then vertex v1 is said to be **adjacent to** v2 while v2 is **adjacent from** v1
- The edge `<v1, v2>` is incident on v1 and v2

**Example:** In G2, vertices 1 and 3 are adjacent to vertex 2, whereas vertex 2 is adjacent from vertex 1.

---

## Graph Representations

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

## Graph Traversals

Given a vertex in a directed or undirected graph, we may wish to visit all vertices reachable from this vertex. This can be done in two ways:

### Depth First Search (DFS)

In this algorithm:
- Start at a vertex and move as far as you can down one path before exploring other paths
- Requires marking vertices to avoid visiting them more than once (using a visited array initialized to false)
- **Pre-order traversal of a binary tree is nothing but a depth first search**

**Procedure for undirected graph:**
1. Start at any vertex v, mark it visited
2. Select an unvisited vertex w adjacent to v and initiate DFS from w
3. When a vertex u is reached where all adjacent vertices have been visited, back up to the last visited vertex with an unvisited adjacent vertex
4. Terminate when no unvisited vertex can be reached from any visited ones

**Example:** Starting from vertex V1, the visit order might be: V1, V2, V4, V8, V5, V6, V3, V7

#### C Implementation:

```c
#include <stdio.h>

void dfs(int a[8][8], int sz, int vis[8], int idx) {
    int i;
    vis[idx] = 1;
    printf("%d ", idx + 1);
    /* go to all columns of idx row */
    for (i = 0; i < sz; i++) {
        if (vis[i] == 0 && a[idx][i] == 1)
            dfs(a, sz, vis, i);
    }
}

int main() {
    int arr[8][8] = {0};
    int visited[8] = {0};
    
    // Setting up adjacency matrix
    arr[0][1] = arr[1][0] = 1;
    arr[0][2] = arr[2][0] = 1;
    arr[1][3] = arr[3][1] = 1;
    arr[1][4] = arr[4][1] = 1;
    arr[2][5] = arr[5][2] = 1;
    arr[2][6] = arr[6][2] = 1;
    arr[3][7] = arr[7][3] = 1;
    arr[4][7] = arr[7][4] = 1;
    arr[5][7] = arr[7][5] = 1;
    arr[6][7] = arr[7][6] = 1;
    
    dfs(arr, 8, visited, 0);
    return 0;
}
```

**Output:** `1 2 4 8 5 6 3 7`

---

### Breadth First Search (BFS)

Starting at vertex v and marking it as visited, BFS differs from DFS in that:
- All unvisited vertices adjacent to v are visited next
- Then unvisited vertices adjacent to these vertices are visited, and so on
- **Level-order traversal of a binary tree is nothing but breadth first search**

**Example:** Beginning at vertex V1, the order would be: V1, then V2 and V3, next V4, V5, V6, and V7, finally V8

#### C Implementation:

```c
#include <stdio.h>
#define MAX 10

struct queue {
    int arr[MAX], front, rear;
};

void addq(struct queue *pq, int item) {
    if (pq->rear == MAX - 1) {
        printf("Queue is full\n");
        return;
    }
    pq->rear++;
    pq->arr[pq->rear] = item;
    if (pq->front == -1)
        pq->front = 0;
}

int delq(struct queue *pq) {
    int data;
    if (pq->front == -1) {
        printf("Queue is Empty\n");
        return NULL;
    }
    data = pq->arr[pq->front];
    pq->arr[pq->front] = 0;
    if (pq->front == pq->rear)
        pq->front = pq->rear = -1;
    else
        pq->front++;
    return data;
}

int isempty(struct queue *pq) {
    if (pq->front == -1 && pq->rear == -1)
        return 1;
    else
        return 0;
}

void bfs(int a[8][8], int sz, int vis[8]) {
    struct queue q;
    int idx, i;
    q.front = q.rear = -1;
    addq(&q, 0);
    
    while (!isempty(&q)) {
        idx = delq(&q);
        if (vis[idx] == 0) {
            vis[idx] = 1;
            printf("%d ", idx + 1);
            for (i = 0; i < sz; i++) {
                if (vis[i] == 0 && a[idx][i] == 1)
                    addq(&q, i);
            }
        }
    }
}

int main() {
    int arr[8][8] = {0};
    int visited[8] = {0};
    
    // Same adjacency matrix setup as DFS
    arr[0][1] = arr[1][0] = 1;
    arr[0][2] = arr[2][0] = 1;
    arr[1][3] = arr[3][1] = 1;
    arr[1][4] = arr[4][1] = 1;
    arr[2][5] = arr[5][2] = 1;
    arr[2][6] = arr[6][2] = 1;
    arr[3][7] = arr[7][3] = 1;
    arr[4][7] = arr[7][4] = 1;
    arr[5][7] = arr[7][5] = 1;
    arr[6][7] = arr[7][6] = 1;
    
    bfs(arr, 8, visited);
    return 0;
}
```

**Output:** `1 2 3 4 5 6 7 8`

---

## Spanning Tree

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

## Shortest Path

A minimal spanning tree gives no indication about the shortest path between two nodes—only the overall cost is minimized. To find the shortest path between two cities/nodes, we use:

### Dijkstra's Algorithm

This algorithm works for both directed and undirected graphs. Kruskal, Prim, and Dijkstra algorithms are **greedy algorithms**—they build a solution piece by piece, making a choice that looks best at every step.

**Steps:**
1. Mark all nodes as unvisited by creating a set of all unvisited nodes
2. Assign distance values—0 to initial node, infinity to others
3. Set the initial node as current node and identify all its unvisited neighbors
4. Calculate neighbor's distances from current node
5. Assign smaller of newly calculated and current distance
6. Mark the current node as visited
7. Set smallest distance unvisited node as new current node
8. Go back to step 3

**Example Result Table:**

| Path | Seq. | Length |
|------|------|--------|
| 1-1 | 1-1 | 7 |
| 1-2 | 1-2 | 5 |
| 1-3 | 1-2-4-3 | 8 |
| 1-4 | 1-2-4 | 7 |

#### C Implementation (Floyd-Warshall variant):

```c
#include <stdio.h>
#define INF 999

int main() {
    int arr[4][4];
    int cost[4][4] = {
        7, 5, 0, 0,
        7, 0, 0, 2,
        0, 3, 0, 0,
        4, 0, 1, 0
    };
    int i, j, k, n = 4;
    
    // Initialize with INF where there's no direct path
    for (i = 0; i < n; i++) {
        for (j = 0; j < n; j++) {
            if (cost[i][j] == 0)
                arr[i][j] = INF;
            else
                arr[i][j] = cost[i][j];
        }
    }
    
    printf("Adjacency matrix of cost of edges:\n");
    for (i = 0; i < n; i++) {
        for (j = 0; j < n; j++)
            printf("%d\t", arr[i][j]);
        printf("\n");
    }
    
    // Floyd-Warshall algorithm
    for (k = 0; k < n; k++) {
        for (i = 0; i < n; i++) {
            for (j = 0; j < n; j++) {
                if (arr[i][j] > arr[i][k] + arr[k][j])
                    arr[i][j] = arr[i][k] + arr[k][j];
            }
        }
    }
    
    printf("Adjacency matrix of lowest cost between the vertices:\n");
    for (i = 0; i < n; i++) {
        for (j = 0; j < n; j++)
            printf("%d\t", arr[i][j]);
        printf("\n");
    }
    return 0;
}
```

---

## Topological Sorting

Topological sorting is a special sorting technique relevant only for a **Directed Acyclic Graph (DAG)**. If a DAG is represented using an array, then after sorting for every directed edge uv, u comes before v in the array.

**Note:** For the same DAG, multiple solutions may exist. Topological sorting is **not the same as DFS**.

**Procedure:**
1. Maintain a boolean array `visited[]` initialized to false
2. Start at a vertex with in-degree 0 (no incoming edges)
3. Perform DFS-like traversal, pushing vertices onto a stack when all their adjacent vertices have been visited
4. Unwind the stack to get the topological order

**Example:**
- **DFS:** 0, 1, 4, 2, 5, 3
- **Topological sort:** 0, 3, 2, 5, 1, 4

---

## Chapter Summary

| Point | Description |
|-------|-------------|
| (a) | There are two types of graphs—directed graph and undirected graph |
| (b) | A graph can be represented using an adjacency matrix, adjacency lists, or adjacency multi-lists |
| (c) | There are two algorithms for graph traversal—depth first search and breadth first search |
| (d) | A spanning tree is an undirected tree consisting of only those edges necessary to connect all vertices |
| (e) | Minimum cost spanning tree can be obtained using Kruskal's algorithm or Prim's algorithm |
| (f) | The shortest path between vertices in a weighted directed graph can be obtained using Dijkstra's algorithm |

---

## Check Your Progress

### Exercise - Level I: True or False

(a) If v1 and v2 are two vertices of a directed graph G, then the edges `<v1,v2>` and `<v2,v1>` represent the same edge.

(b) For a graph there can exist only those many spanning trees as the number of vertices.

(c) To find minimum cost spanning tree edges are inserted in increasing order of their cost.

(d) The number of elements in the adjacency matrix of a graph having 6 vertices is 36.

(e) If V is the number of vertices and E is the number of edges, the time complexity to calculate the number of edges using an adjacency matrix is O(V²).

(f) If V is the number of vertices and E is the number of edges, time Complexity of Depth First Search is O(V+E).

(g) If V is the number of vertices and E is the number of edges, time Complexity of Breadth First Search is O(V+E).

(h) Adjacency matrix of any graph is always symmetric.

(i) Dijkstra's Algorithm works for both negative and positive weights.

---

### Exercise - Level II: Multiple Choice

(a) For an adjacency matrix of a directed graph the row sum is the ______ degree of a vertex and the column sum is the ______ degree of the vertex.
- (1) in, out
- (2) out, in
- (3) in, total
- (4) total, out

(b) What is the maximum number of possible non-zero values in an adjacency matrix of a simple graph with n vertices?
- (1) n*(n-1)/2
- (2) n*(n+1)/2
- (3) n*(n-1)
- (4) n*(n+1)

(c) Breadth First Search is equivalent to which traversal in Binary Trees?
- (1) Pre-order Traversal
- (2) Post-order Traversal
- (3) Level-order Traversal
- (4) In-order Traversal

(d) Depth First Search is equivalent to which binary tree traversal?
- (1) Pre-order Traversal
- (2) Post-order Traversal
- (3) Level-order Traversal
- (4) In-order Traversal

(e) The data structure used in implementation of Breadth First Search is:
- (1) Stack
- (2) Queue
- (3) Linked List
- (4) None of the mentioned

(f) The data structure used in implementation of Depth First Search is:
- (1) Stack
- (2) Queue
- (3) Linked List
- (4) None of the mentioned

(g) Joshi wants to visit 5 cities starting from Mumbai with an aim to minimize the cost of travel. Which algorithm should he use?
- (1) Depth First Search
- (2) Kruskal's algorithm
- (3) Prim's algorithm
- (4) Dijkstra's algorithm

---

### Exercise - Level III: Coding Questions

(a) What would be the sequence of nodes if the graph shown in Figure 8-14(a) is traversed using DFS algorithm starting at vertex 6?

(b) What would be the sequence of nodes if the graph shown in Figure 8-14(b) is traversed using BFS algorithm starting at vertex 5?

(c) Create a minimum spanning tree for graph shown in Figure 8-14(c) using Kruskal's algorithm.

(d) Create a minimum spanning tree for graph shown in Figure 8-14(c) using Prim's algorithm.

(e) If a graph is represented using an adjacency matrix, write a program that finds:
- The number of vertices in a graph
- The number of adjacent vertices for a given vertex

---

### Case Scenario Exercise

**Kruskal's and Prim's algorithm**

Write a program to implement Kruskal's and Prim's algorithms. Also analyze the time complexity of each.

---
*Source: Data Structures Through C, 4th Edition, Chapter 8: Graphs (Pages 211-236)*
```