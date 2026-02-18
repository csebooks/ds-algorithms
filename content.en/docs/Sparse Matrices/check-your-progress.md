---
title: Check Your Progress
weight: 9
---

### Exercise - Level I

**[A] Pick up the correct alternative for each of the following questions:**

(f) A matrix is called sparse when
1. Most of its elements are non-zero
2. Most of its elements are zero
3. All of its elements are non-zero
4. None of the above

(g) In the linked representation of a sparse matrix the head node for a column list stores
1. A pointer to the next column head node
2. A pointer to the first node in column list
3. Column number
4. All of the above

(h) A sparse matrix can be lower-triangular matrix
1. When all the non-zero elements lie only on the leading diagonal.
2. When all the non-zero elements lie above leading diagonal.
3. When all the non-zero elements lie below leading diagonal.
4. Both (3) and (4)

---

### Exercise - Level II

**[B] Answer the following:**

(a) Write a program to build a sparse matrix as an array. Write functions to check if the sparse matrix is a square, diagonal, lower triangular, upper triangular or tridiagonal matrix.

(b) Write a program to subtract two sparse matrices implemented as an array.

(c) Write a program to build a sparse matrix as a linked list. The program should provide functions for following operations:
   - (i) Store an element when the row number, column number and the value is provided
   - (ii) Retrieve an element for given row and column of matrix
   - (iii) Add two sparse matrices
   - (iv) Subtract two sparse matrices

---

### Exercise Level III: Coding Interview Questions

Write a program that carries out multiplication of two sparse matrices through their 3-tuple form and stores the result in another sparse matrix in 3-tuple form.

---

### Case Scenario Exercise: Linked representation of Sparse Matrix

Write a program that stores sparse matrix in the linked list form. The skeleton code for this program is given below. You are required to define different functions whose prototypes are given in the skeleton code and then call these functions from main().

```c
#define MAX1 3
#define MAX2 3

/* structure for col head node */
struct cheadnode {
    int colno;
    struct node *down;
    struct cheadnode *next;
};

/* structure for row head node */
struct rheadnode {
    int rowno;
    struct node *right;
    struct rheadnode *next;
};

/* structure for node to store element */
struct node {
    int row, col, val;
    struct node *right;
    struct node *down;
};

/* structure for special head node */
struct spmat {
    struct rheadnode *firstrow;
    struct cheadnode *firstcol;
    int noofrows;
    int noofcols;
};

struct sparse {
    int *sp;
    int row;
    struct spmat *smat;
    struct cheadnode *chead[MAX2];
    struct rheadnode *rhead[MAX1];
    struct node *nd;
};

void initsparse(struct sparse *);
void create_array(struct sparse *);
void display(struct sparse);
int count(struct sparse);
void create_triplet(struct sparse *, struct sparse);
void create_llist(struct sparse *);
void insert(struct sparse *, struct spmat *, int, int, int);
void show_llist(struct sparse);
void delsparse(struct sparse *);
```
```