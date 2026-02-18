---
title: Linked Representation of a Sparse Matrix
weight: 6
---

Representing a sparse matrix as an array of 3-tuples suffers from one important limitation. When we carry out addition or multiplication it is not possible to predict beforehand how many elements in the resultant matrix would be non-zero. As a result, it is not possible to predict the size of the resultant matrix beforehand. Instead of an array we can represent the sparse matrix in the form of a linked list.

In the linked list representation, a separate list is maintained for each column as well as each row of the matrix, i.e., if the matrix is of size 3 x 3, then there would be 3 lists for 3 columns and 3 lists for 3 rows. A node in a list stores the information about the non-zero element of the sparse matrix. The head node for a column list stores the column number, a pointer to the node, which comes first in the column, and a pointer to the next column head node. Thus, the structure for column head node would be as shown below:

```c
struct cheadnode {
    struct node *down;
    int colno;
    struct cheadnode *next;
};
```

A head node for a row list stores, a pointer to the node, which comes first in the row list, and a pointer to the next row head node. The structure for row head node would be as shown below:

```c
struct rheadnode {
    struct rheadnode *next;
    int rowno;
    struct node *right;
};
```

A node on the other hand stores the row number, column number and the value of the non-zero element of the sparse matrix. It also stores a pointer to the node that is immediately to the right of the node in the row list as well as a pointer to the node that is immediately below the node in the column list. The structure for a node would be as shown below:

```c
struct node {
    int row;
    int col;
    int val;
    struct node *down;
    struct node *right;
};
```

In addition to this a special node is used to store the total number of rows, total number of columns, a pointer to the first row head node and a pointer to the first column head node. The information stored in this special node is used for traversing the list. The structure of this special node would be as shown below:

```c
struct spmat {
    struct rheadnode *firstrow;
    int noofrows;
    int noofcols;
    struct cheadnode *firstcol;
};
```

If a particular column list is empty then the field `down` of the column head node would be NULL. Similarly, if a row list is empty then the field `right` of the row head node would be empty. If a node is the last node in a particular column list or a particular row list then the field `down` or the field `right` of the node would be NULL.

Figure 4-2 gives pictorial representation of linked list of a sparse matrix of size 3×3.

**Figure 4-2: Linked Representation of a sparse matrix**

```
Special Head Node
┌─────────┬─────┬─────┐
│ firstrow│  3  │first│  noofrows=3, noofcols=3
│   ↓     │     │col  │
└────┬────┴─────┴──┬──┘
     │             │
     ▼             ▼
rhead[0]      chead[0]
┌─────┬───┬───┐   ┌───┬───┬───┐
│next │ 0 │right│   │down│ 0 │next│
│  ↓  │   │  ↓  │   │ ↓  │   │ ↓  │
└──┬──┴───┴──┬──┘   └──┬─┴───┴──┬─┘
   │         │         │        │
   ▼         ▼         ▼        ▼
rhead[1]   [0,0,2]   [0,0,2]  chead[1]
┌─────┬───┬───┐   ┌───┬───┐   ┌───┬───┬───┐
│next │ 1 │right│   │ N │ N │   │ N │ 1 │next│
│  ↓  │   │  ↓  │   └───┴───┘   │   │   │ ↓  │
└──┬──┴───┴──┬──┘               └───┴───┴──┬─┘
   │         │                              │
   ▼         ▼                              ▼
rhead[2]   [1,0,11]                      chead[2]
┌─────┬───┬───┐                           ┌───┬───┬───┐
│  N  │ 2 │right│                          │   │ 2 │ N │
└─────┴───┴───┘                           └───┴───┴───┘
                │
                ▼
           [0,2,7]
           ┌───┬───┐
           │ N │ N │
           └───┴───┘
```

---