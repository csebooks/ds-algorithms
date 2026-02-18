---
title: Operations on a Binary Search Tree
weight: 5
---

There are many operations that can be performed on binary search trees. **Insertion, Traversal, Searching and Deletion** are the most basic amongst them.

### Insertion of a Node

While inserting a node in a BST the value being inserted is compared with the root node. A left sub-tree is taken if the value is smaller than the root node and a right sub-tree if it is greater or equal to the node. This operation is repeated at each level till a node is found whose left or right sub-tree is empty. Finally, the new node is appropriately made the left or right child of this node.

If the input list is 3, 9, 1, 4, 7, 11, then Figure 7-8 shows the stepwise insertion of new nodes in a BST.

![Figure 7-8: Creation of a Binary Search Tree](image-placeholder)

### Traversal of a BST

The traversal of a BST is to visit each node in the tree exactly once. There are three popular methods of BST traversal:

| Traversal | Order of Operations |
|-----------|-------------------|
| **Pre-order** | (1) Visit the root <br> (2) Traverse the left sub-tree in pre-order <br> (3) Traverse the right sub-tree in pre-order |
| **In-order** | (1) Traverse the left sub-tree in in-order <br> (2) Visit the root <br> (3) Traverse the right sub-tree in in-order |
| **Post-order** | (1) Traverse the left sub-tree in post-order <br> (2) Traverse the right sub-tree in post-order <br> (3) Visit the root |

In each of these methods nothing needs be done to traverse an empty BST.

![Figure 7-9: Traversals of binary tree](image-placeholder)

**Example from Figure 7-9:**
- Inorder: 5, 6, 7, 8, 10, 13, 17, 18, 20
- Preorder: 20, 17, 6, 5, 8, 7, 10, 13, 18
- Postorder: 5, 7, 13, 10, 8, 6, 18, 17, 20

### Searching of a Node

To search any node in a binary tree, initially the value to be searched is compared with the root node. If they match then the search is successful. If the value is greater than the root node then searching process proceeds in the right sub-tree of the root node, otherwise, it proceeds in the left sub-tree of the root node.

BST search operation is very efficient because while searching an element we do not need to traverse the entire tree. At every node, we get a hint regarding which sub-tree to search in. Since at every step we eliminate half of the sub-tree from the search process the **average search time is O(log₂n)**. Same applies to insertion or deletion of an element in a BST.

As against this, in a sorted array, even though searching can be done in O(log₂n) time, insertion and deletion times are high. In contrast, insertion and deletion of elements in a linked list is easier, but searching takes O(n).

Due to this efficiency BSTs are widely used in dictionary problems where insertion, deletion and search are done on the basis of some indexed key.

### Deletion of a Node

While deleting a node from a BST there are four possible cases that we need to consider:

**Case (a): Node to be deleted is not found**
If on traversing the BST the node is not found then we merely need to display the message that the node is not found.

**Case (b): Node to be deleted has no children**
In this case since the node to be deleted has no children the memory occupied by it should be freed and either the left link or the right link of the parent of this node should be set to NULL. Which link should be set to NULL depends upon whether the node being deleted is a left child or a right child of its parent.

**Case (c): Node to be deleted has one child**
In this case we have to adjust the pointer of the parent of the node to be deleted such that after deletion it points to the child of the node being deleted.

![Figure 7-10: Deletion of a node that has only one child](image-placeholder)

**Case (d): Node to be deleted has two children**
This is a more complex case. Consider node 23 shown in Figure 7-11(a). The **in-order successor** of the node 23 is node 45. The in-order successor should now be copied into the node to be deleted and a pointer should be set up pointing to the in-order successor (node 45). The in-order successor would always have one or zero child. This in-order successor should then be deleted using the same procedure as for deleting a one child or a zero-child node.

![Figure 7-11: Deletion of a node that has both left and right child](image-placeholder)

---

### Program 7-1: Implementation of various BST operations

```c
#include <stdio.h>
#include <stdlib.h>

#define TRUE 1
#define FALSE 0

struct btreenode {
    struct btreenode *leftchild;
    int data;
    struct btreenode *rightchild;
};

void insert(struct btreenode **, int);
void inorder(struct btreenode *);
void preorder(struct btreenode *sr);
void postorder(struct btreenode *sr);
int search(struct btreenode *, int);
void del(struct btreenode **, int);
void locate(struct btreenode **, int, struct btreenode **, 
            struct btreenode **, int *);

int main() {
    struct btreenode *bt;
    int i = 0, a[] = {20, 17, 6, 18, 8, 5, 7, 10, 13};
    int flag;
    
    bt = NULL; /* empty tree */
    
    while (i <= 8) {
        insert(&bt, a[i]);
        i++;
    }
    
    printf("BST after insertion:");
    printf("\nInorder: ");
    inorder(bt);
    printf("\nPreorder: ");
    preorder(bt);
    printf("\nPostorder: ");
    postorder(bt);
    
    flag = search(bt, 13);
    if (flag == 1)
        printf("\nNode 13 found in BST");
    else
        printf("\nNode 13 not found in BST");
    
    del(&bt, 10);
    printf("\nBST after deleting 10:\n");
    inorder(bt);
    
    del(&bt, 14);
    printf("\nBST after deleting 14:\n");
    inorder(bt);
    
    del(&bt, 8);
    printf("\nBST after deleting 8:\n");
    inorder(bt);
    
    del(&bt, 13);
    printf("\nBinary tree after deleting 13:\n");
    inorder(bt);
    
    return 0;
}

/* inserts a new node in BST */
void insert(struct btreenode **sr, int num) {
    if (*sr == NULL) {
        *sr = (struct btreenode *)malloc(sizeof(struct btreenode));
        (*sr)->leftchild = NULL;
        (*sr)->data = num;
        (*sr)->rightchild = NULL;
    } else {
        /* search the node to which new node will be attached */
        /* if new data is less, traverse to left */
        if (num < (*sr)->data)
            insert(&((*sr)->leftchild), num);
        else
            /* else traverse to right */
            insert(&((*sr)->rightchild), num);
    }
}

/* traverse BST in Left-Root-Right fashion */
void inorder(struct btreenode *sr) {
    if (sr != NULL) {
        inorder(sr->leftchild);
        printf("%d ", sr->data);
        inorder(sr->rightchild);
    }
}

/* traverse BST in Root-Left-Right fashion */
void preorder(struct btreenode *sr) {
    if (sr != NULL) {
        printf("%d ", sr->data);
        preorder(sr->leftchild);
        preorder(sr->rightchild);
    }
}

/* traverse BST in Left-Right-Root fashion */
void postorder(struct btreenode *sr) {
    if (sr != NULL) {
        postorder(sr->leftchild);
        postorder(sr->rightchild);
        printf("%d ", sr->data);
    }
}

/* search BST */
int search(struct btreenode *sr, int num) {
    while (sr != NULL) {
        if (num == sr->data)
            return 1;
        else if (num < sr->data)
            sr = sr->leftchild;
        else
            sr = sr->rightchild;
    }
    return 0;
}

/* deletes a node from the BST */
void del(struct btreenode **root, int num) {
    int found;
    struct btreenode *parent, *x, *xsucc;
    
    /* if tree is empty */
    if (*root == NULL) {
        printf("Tree is empty\n");
        return;
    }
    
    parent = x = NULL;
    
    /* search the node to be deleted */
    locate(root, num, &parent, &x, &found);
    
    /* if the node to deleted is not found */
    if (found == FALSE) {
        printf("\nNode to be deleted not found\n");
        return;
    }
    
    /* if the node to be deleted has two children */
    if (x->leftchild != NULL && x->rightchild != NULL) {
        parent = x;
        xsucc = x->rightchild;
        while (xsucc->leftchild != NULL) {
            parent = xsucc;
            xsucc = xsucc->leftchild;
        }
        x->data = xsucc->data;
        x = xsucc;
    }
    
    /* if the node to be deleted has no child */
    if (x->leftchild == NULL && x->rightchild == NULL) {
        if (parent->rightchild == x)
            parent->rightchild = NULL;
        else
            parent->leftchild = NULL;
        free(x);
        return;
    }
    
    /* if the node to be deleted has only right child */
    if (x->leftchild == NULL && x->rightchild != NULL) {
        if (parent->leftchild == x)
            parent->leftchild = x->rightchild;
        else
            parent->rightchild = x->rightchild;
        free(x);
        return;
    }
    
    /* if the node to be deleted has only left child */
    if (x->leftchild != NULL && x->rightchild == NULL) {
        if (parent->leftchild == x)
            parent->leftchild = x->leftchild;
        else
            parent->rightchild = x->leftchild;
        free(x);
        return;
    }
}

/* returns address of the node to be deleted, address of its parent and 
   whether node is found or not */
void locate(struct btreenode **root, int num, struct btreenode **par,
            struct btreenode **x, int *found) {
    struct btreenode *q;
    q = *root;
    *found = FALSE;
    *par = NULL;
    
    while (q != NULL) {
        /* if the node to be deleted is found */
        if (q->data == num) {
            *found = TRUE;
            *x = q;
            return;
        }
        *par = q;
        if (q->data > num)
            q = q->leftchild;
        else
            q = q->rightchild;
    }
}
```

**Output:**
```
BST after insertion:
Inorder: 5 6 7 8 10 13 17 18 20 
Preorder: 20 17 6 5 8 7 10 13 18 
Postorder: 5 7 13 10 8 6 18 17 20 
Node 13 found in BST
BST after deleting 10:
5 6 7 8 13 17 18 20 
Node to be deleted not found
BST after deleting 14:
5 6 7 8 13 17 18 20 
BST after deleting 8:
5 6 7 13 17 18 20 
Binary tree after deleting 13:
5 6 7 17 18 20 
```

---