---
title: Shortest Path
weight: 7
---

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