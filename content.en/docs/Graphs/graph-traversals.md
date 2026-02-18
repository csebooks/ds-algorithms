---
title: Graph Traversals
weight: 5
---

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