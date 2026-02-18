---
title: 'Trees'
weight: 7
references:
    books:
        - b1:
            title: Data Structures and Algorithm Analysis in C by Mark Allen Weiss 
            url: https://mrajacse.files.wordpress.com/2012/08/data-structures-and-algorithm-analysis-in-c-mark-allen-weiss.pdf
        - b2:
            title: Data_Structures_and_Algorithm_Analysis_2e By mark-allen-weiss
            url: https://www.google.co.in/books/edition/Data_Structures_and_Algorithm_Analysis_i/83RWbPynhkgC?hl=en&gbpv=1

---
I'll convert this PDF about Trees in Data Structures to Markdown format for you.

```markdown
# Chapter 7: Trees

## Trees Of Herbs, Shrubs and Bushes

### Why This Chapter Matters?

Nature is man's best teacher. In every walk of life man has explored nature, learnt his lessons and then applied the knowledge that nature offered him to solve every-day problems that he faced at workplace. It isn't without reason that there are data structures like Trees, Binary Trees, Search Trees, AVL Trees, Forests, etc. Trees are non-linear data structures. They have many applications in Computer Science, hence you must understand them.

---

If large input data is stored in a linked list, then time required to access the data is prohibitive. In such cases a data structure called Tree is used. This data structure is often used in constructing the file systems and evaluation of arithmetic expressions. This data structure gives a running time of O(log n) for most operations.

Like linked lists, a tree also consists of several nodes. Each node may contain links that point to other nodes in the tree. So a tree can be used to represent a person and all of his descendants as shown in Figure 7-1.

![Figure 7-1: A tree structure](image-placeholder)

Note that each node in this tree contains a name for data and one or more pointers to the other tree nodes. Although a tree may contain any number of pointers to the other tree nodes, a large number of have at the most two pointers to the other tree nodes. Such trees are called **Binary trees**.

---

## Binary Trees

Let us begin our study of binary trees by discussing some basic concepts and terminology.

A **binary tree** is a finite set of elements that is either empty or is partitioned into three disjoint sub-sets. The first sub-set contains a single element called the **root** of the tree. The other two sub-sets are themselves binary trees, called the **left** and **right sub-trees** of the original tree. A left or right sub-tree can be empty.

Each element of a binary tree is called a **node** of the tree. The tree shown in Figure 7-2(a) consists of nine nodes with A as its root. Its left sub-tree is rooted at B and its right sub-tree is rooted at C. This is indicated by the two branches emanating from A to B on the left and to C on the right. The absence of a branch indicates an empty sub-tree. For example, the left sub-tree of the binary tree rooted at C and the right sub-tree of the binary tree rooted at E are both empty. The binary trees rooted at D, G, H and I have empty right and left sub-trees.

Figure 7-2(b) illustrates a structure that is **not** a binary tree.

![Figure 7-2: Binary tree](image-placeholder)

### Terminology

Let us now learn some terminology used in association with binary trees.

- **Parent, Child**: If A is the root of a binary tree and B is the root of its left or right sub-tree then, A is parent of B and B is left or right child of A.

- **Leaf**: A node that has no children (such as D, G, H, or I in Figure 7-2(a)) is called a leaf.

- **Ancestor, Descendant**: Any node n1, is an ancestor of node n2 (and n2 is a descendant of n1) if n1 is either the parent of n2 or the parent of some ancestor of n2. For example, in the tree shown in Figure 7-2(a), A is an ancestor of C.

- **Climbing, Descending**: The root of the tree is at the top and the leaves at the bottom. Going from the leaves to the root is called climbing the tree, and going from the root to the leaves is called descending the tree.

- **Degree of a node**: The number of nodes connected to a particular node is called the degree of a particular node. For example, in Figure 7-2(a) the node B has a degree 3. The degree of a leaf node is always one.

- **Level**: The root of the tree has level 0. Level of any other node in the tree is one more than the level of its parent. For example, in the binary tree shown in Figure 7-2(a), node E is at level 2 and node H is at level 3.

- **Depth**: Depth of a node is the maximum number of links from root to that node. The depth of a binary tree is the maximum level of any leaf in the tree. This equals the length of the longest path from the root to any leaf. Thus, the depth of the tree shown in Figure 7-2(a) is 3.

- **Height**: Height of a node is the maximum number of links from that node to leaf node. Height of a binary tree is height of its root node.

- **Strictly binary tree**: If every non-leaf node in a binary tree has nonempty left and right sub-trees, the tree is termed a strictly binary tree. Thus, the tree shown in Figure 7-3(a) is a strictly binary tree.

- **Complete binary tree**: A complete binary tree (refer Figure 7-3(b)) has maximum number of possible nodes at all levels except the last level, and all the nodes of the last level appear as far left as possible.

![Figure 7-3: Strictly and Complete binary tree](image-placeholder)

---

## Representation of Binary Trees in Memory

There are two ways by which we can represent a binary tree—**Linked representation** and **Array representation**. Both these ways are discussed below.

### Linked Representation of Binary Trees

In linked representation each node contains addresses of its left child and right child. If a child is absent, the link contains a NULL value. For example, in Figure 7-4 the link fields of node C contain the address of the nodes F and G. The left link field of node E contains the address of the node H. Similarly, the right link contains a NULL as E has no right child. The nodes D, F, G and H contain a NULL value in both their link fields, as these are the leaf nodes.

![Figure 7-4: Linked representation of a Binary tree](image-placeholder)

### Array Representation of Binary Trees

When a binary tree is represented by arrays three separate arrays are required. One array `arr` stores the data fields of the trees. The other two arrays `lc` and `rc` represents the left child and right child of the nodes. Figure 7-5 shows these three arrays, which represents the tree shown in Figure 7-4.

![Figure 7-5: Array representation of a binary tree](image-placeholder)

The array `lc` and `rc` contains the index of the array `arr` where the data is present. If the node does not have any left child or right child then the element of the array `lc` or `rc` contains a value -1. The 0th element of the array `arr` contains the root node data. Some elements of the array `arr` contain `'\0'` which represents an empty child.

Suppose we wish to find the left and right child of the node E. Then we need to find the value present at index 4 in array `lc` and `rc` since E is present at index 4 in the array `arr`. The value present at index 4 in the array `lc` is 9, which is the index position of node H in the array `arr`. So, the left child of the node E is H. The right child of the node E is empty because the value present at index 4 in the array `rc` is –1.

We can also represent a binary tree using one single array. For this, numbers are given to each node starting from the root node—0 to root node, 1 to the left node of the first level, then 2 to the second node from left of the first level and so on. In other words, the nodes are numbered from left to right level by level from top to bottom. Figure 7-6(a) shows the numbers given to each node in the tree. Note that while numbering the nodes of the tree, empty nodes are also taken into account.

![Figure 7-6: Array representation of binary tree using one array](image-placeholder)

It can be observed that if n is the number given to the node, then its left child is at position (2n+1) in the array and right child at position (2n + 2). If any node doesn't have a left or a right child then an empty node is assumed and a value `'\0'` is stored at that index in the array.

---

## Binary Search Trees

Binary search tree (BST) is a variant of binary tree in which the nodes are arranged in a particular manner. A BST has the property that all the elements in the left sub-tree of a node n are less than n and all the elements in the right sub-tree of n are greater than or equal to n. Figure 7-7 shows a few examples.

![Figure 7-7: Sample BSTs](image-placeholder)

---

## Operations on a Binary Search Tree

There are many operations that can be performed on binary search trees. **Insertion, Traversal, Searching** and **Deletion** are the most basic amongst them. Let us now discuss these operations in detail.

### Insertion of a Node

While inserting a node in a BST the value being inserted is compared with the root node. A left sub-tree is taken if the value is smaller than the root node and a right sub-tree if it is greater or equal to the node. This operation is repeated at each level till a node is found whose left or right sub-tree is empty. Finally, the new node is appropriately made the left or right child of this node.

If the input list is 3, 9, 1, 4, 7, 11, then Figure 7-8 shows the stepwise insertion of new nodes in a BST.

![Figure 7-8: Creation of a Binary Search Tree](image-placeholder)

### Traversal of a BST

The traversal of a BST is to visit each node in the tree exactly once. There are three popular methods of BST traversal—**in-order traversal, pre-order traversal** and **post-order traversal**. In each of these methods nothing needs be done to traverse an empty BST.

Recall that each sub-tree of a BST is a BST itself. Thus, traversing a BST involves visiting the root node and traversing its left and right sub-trees. The only difference among the methods is the order in which these three operations are performed.

**To traverse a non-empty BST in pre-order**, we perform the following three operations:
1. Visit the root
2. Traverse the left sub-tree in pre-order
3. Traverse the right sub-tree in pre-order

**To traverse a non-empty BST in in-order** (or symmetric order):
1. Traverse the left sub-tree in in-order
2. Visit the root
3. Traverse the right sub-tree in in-order

**To traverse a non-empty BST in post-order**:
1. Traverse the left sub-tree in post-order
2. Traverse the right sub-tree in post-order
3. Visit the root

Figure 7-9 shows the order of visiting nodes using these traversal methods for the given BST.

![Figure 7-9: Traversals of binary tree](image-placeholder)

### Searching of a Node

To search any node in a binary tree, initially the value to be searched is compared with the root node. If they match then the search is successful. If the value is greater than the root node then searching process proceeds in the right sub-tree of the root node, otherwise, it proceeds in the left sub-tree of the root node.

BST search operation is very efficient because while searching an element we do not need to traverse the entire tree. At every node, we get a hint regarding which sub-tree to search in. For example, in the BST shown in Figure 7-8 step 6, if we have to search for 7, then we know that we have to scan only the right sub-tree since 7 is greater than 3. Likewise, when we descend down the tree and reach 9 we have to search only its left sub-tree as 7 is less than 9.

Since at every step we eliminate half of the sub-tree from the search process the average search time is O(log₂n). Same applies to insertion or deletion of an element in a BST. As against this, in a sorted array, even though searching can be done in O(log₂n) time, insertion and deletion times are high. In contrast, insertion and deletion of elements in a linked list is easier, but searching takes O(n).

Due to this efficiency BSTs are widely used in dictionary problems where insertion, deletion and search are done on the basis of some indexed key.

### Deletion of a Node

While deleting a node from a BST there are four possible cases that we need to consider. These are discussed below.

**Case (a): Node to be deleted is not present**
If on traversing the BST the node is not found then we merely need to display the message that the node is not found.

**Case (b): Node to be deleted has no children**
In this case since the node to be deleted has no children the memory occupied by it should be freed and either the left link or the right link of the parent of this node should be set to NULL. Which link should be set to NULL depends upon whether the node being deleted is a left child or a right child of its parent.

**Case (c): Node to be deleted has one child**
In this case we have to adjust the pointer of the parent of the node to be deleted such that after deletion it points to the child of the node being deleted. This is shown in Figure 7-10.

![Figure 7-10: Deletion of a node that has only one child](image-placeholder)

**Case (d): Node to be deleted has two children**
This is a more complex case. Consider node 23 shown in Figure 7-11(a). The **in-order successor** of the node 23 is node 45. The in-order successor should now be copied into the node to be deleted and a pointer should be set up pointing to the in-order successor (node 45). The in-order successor would always have one or zero child. This in-order successor should then be deleted using the same procedure as for deleting a one child or a zero-child node.

![Figure 7-11: Deletion of a node that has both left and right children](image-placeholder)

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
void locate(struct btreenode **, int, struct btreenode **, struct btreenode **, int *);

int main() {
    struct btreenode *bt;
    int i = 0, a[] = {20, 17, 6, 18, 8, 5, 7, 10, 13};
    int flag;
    
    bt = NULL;  /* empty tree */
    
    while (i <= 8) {
        insert(&bt, a[i]);
        i++;
    }
    
    printf("BST after insertion:");
    printf("\nInorder:");
    inorder(bt);
    printf("\nPreorder:");
    preorder(bt);
    printf("\nPostorder:");
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
    }
    else {  /* search the node to which new node will be attached */
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

### Output:
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

### Explanation

In `main()`, `bt`, the pointer to the root node of BST is set to NULL indicating the BST is empty to begin with. Then the `insert()` function is called repeatedly to insert nodes in the BST. Two arguments are passed to `insert()`—address of pointer to the root node of BST and data that is to be inserted.

In the `insert()` function it is ascertained whether BST is empty or not. If it is empty then a new node is created and the data to be inserted is stored in it. The left and right child of this new node is set with a NULL value, as this is the first node being inserted.

If BST is not empty then the current node is compared with the data to be inserted and `insert()` function is called recursively to insert the node in the left/right sub-tree. Thus `insert()` continues to move down the levels of BST until it reaches a leaf node. When it does, the new node gets inserted in the left/right sub-tree.

The function `inorder()` is called to traverse BST as per in-order traversal. This function receives address of the root node. A condition is checked whether the pointer is NULL. If the pointer is not NULL then a recursive call is made first for traversing the left sub-tree and then for traversing the right sub-tree. In between these two recursive calls, the data of the current node is printed.

The functions `preorder()` and `postorder()` work in the same manner except for a small difference. In case of the function `preorder()` initially node's data is printed then the recursive calls are made for the left and right sub-trees. On the other hand, in case of `postorder()` firstly the recursive calls for left and right sub-trees are made and then the node's data is printed.

The function `search()` searches for the given data in the BST. The searching is done in a while loop. If the node is found then 1 is returned. If not, then we either go to the left or right sub-tree depending upon whether the node being searched has a value less than or greater than the current node's data. If control goes beyond the while loop it means that node being searched is not present in the BST. In this case 0 is returned.

The `del()` function is used to delete a node in BST. It calls the function `locate()` to search the node to be deleted. If the node is found, `locate()` sets up the address of the node to be deleted in `x`, address of its parent in `parent` and TRUE/FALSE in `found` depending upon whether the node is found or not. If node to be deleted is not found then an appropriate message is printed.

If the node to be deleted is found then one of the following four cases would arise:
- (a) the node has two children
- (b) the node has no child
- (c) the node has only right child
- (d) the node has only left child

---

## Reconstruction of a Binary Tree

If we know the sequence of nodes obtained through in-order/preorder/post-order traversal it may not be feasible to reconstruct the binary tree. This is because two different binary trees may yield same sequence of nodes when traversed using post-order traversal. Similarly, in-order or pre-order traversal of different binary trees may yield the same sequence of nodes. However, we can construct a unique binary tree if the results of in-order and pre-order traversal are available. Let us understand this with the help of following set of in-order and pre-order traversal results:

- **In-order traversal**: 4, 7, 2, 8, 5, 1, 6, 9, 3
- **Pre-order traversal**: 1, 2, 4, 7, 5, 8, 3, 6, 9

We know that the first value in the pre-order traversal gives us the root of the binary tree. So, the node with data 1 becomes the root of the binary tree. In in-order traversal, initially the left sub-tree is traversed then the root node and then the right sub-tree. So, the data before 1 in the in-order list (i.e. 4, 7, 2, 8, 5) forms the left sub-tree and the data after 1 in the in-order list (i.e. 6, 9, 3) forms the right sub-tree. In Figure 7-12(a) the structure of tree is shown after separating the tree in left and right sub-trees.

![Figure 7-12: Reconstruction of a binary tree](image-placeholder)

Now look at the left sub-tree. The data in pre-order list is 2, so the root node of the left sub-tree is 2. Hence data before 2 in the in-order list (i.e., 4, 7) will form the left sub-tree of the node that contains a value 2. The data that comes to the right of 2 in the in-order list (i.e., 8, 5) forms the right sub-tree of the node with value 2. Figure 7-12(b) shows structure of tree after expanding the left and right sub-tree of the node that contains a value 2.

Now the next data in pre-order list is 4, so the root node of the left subtree of the node that contains a value 2 is 4. The data before 4 in the inorder list forms the left sub-tree of the node that contains a value 4. But as there is no data present before 4 in in-order list, the left sub-tree of the node with value 4 is empty. The data that comes to the right of 4 in the in-order list (i.e., 7) forms the right sub-tree of the node that contains a value 4. Figure 7-12(c) shows structure of tree after expanding the left and right sub-tree of the node that contains a value 4.

In the same way one by one all the data are picked from the pre-order list and are placed and their respective sub-trees are constructed. Figure 7-12(d) to 7-12(f) shows each step of this construction process.

---

## Threaded Binary Tree

In the linked representation of a binary tree, many nodes contain a NULL pointer, either in their left or right fields or in both. Instead of wasting space in storing a NULL pointer, it can be efficiently used to store pointer to the in-order predecessor or the in-order successor of the node. These special pointers are called **threads** and binary trees containing threads are called **threaded binary trees**.

In threaded binary trees the pointers that point to in-order successor of a node are called **right threads**. Likewise, pointers that point to in-order predecessor of a node are called **left threads**. The threads are typically denoted using arrows as shown in Figure 7-13.

![Figure 7-13: Threaded binary tree](image-placeholder)

Figure 7-13(b) shows a head node containing a value -999. The entire binary tree is shown as the left child of this head node. The right link of the head node points to itself. This head node is useful while creating programs for threaded binary tree. For example, while traversing the tree we can start with head node, visit each node and stop the traversal when we reach the head node once again. Note that in Figure 7-13(b) predecessor of node D and successor of node I point to the head node as they happen to be first and last node in the in-order traversal sequence.

In a program to help us distinguish between a pointer and a thread, the structure that represents a node contains two additional fields, `leftflag` and `rightflag`. If they contain a true, they represent a thread, and if they contain a false, then they represent a pointer to a child node. The structure declaration for a node would be as shown below.

```c
struct thtree {
    enum boolean leftflag;
    struct thtree *left;
    int data;
    struct thtree *right;
    enum boolean rightflag;
};
```

A threaded binary tree created using this structure is shown in Figure 7-14.

![Figure 7-14: Threaded binary tree showing links and threads](image-placeholder)

---

### Program 7-2: Implementation of threaded binary tree

```c
#include <stdio.h>
#include <stdlib.h>

enum boolean {link, thread};

struct thtree {
    enum boolean leftflag;
    struct thtree *left;
    int data;
    struct thtree *right;
    enum boolean rightflag;
};

void insert(struct thtree **, int);
void inorder(struct thtree *);

int main() {
    struct thtree *th_head;
    th_head = NULL;  /* empty tree */
    
    insert(&th_head, 11);
    insert(&th_head, 9);
    insert(&th_head, 13);
    insert(&th_head, 8);
    insert(&th_head, 10);
    insert(&th_head, 12);
    insert(&th_head, 14);
    insert(&th_head, 15);
    insert(&th_head, 7);
    
    printf("Threaded binary tree:\n");
    inorder(th_head);
    
    return 0;
}

/* inserts a node in a threaded binary tree */
void insert(struct thtree **s, int num) {
    struct thtree *head, *p, *z;
    
    z = (struct thtree *)malloc(sizeof(struct thtree));
    z->leftflag = thread;
    z->data = num;
    z->rightflag = thread;
    
    /* if tree is empty */
    if (*s == NULL) {
        head = (struct thtree *)malloc(sizeof(struct thtree));
        /* entire tree is treated as left sub-tree of the head node */
        head->leftflag = link;
        head->left = z;  /* z becomes leftchild of the head node */
        head->data = -9999;  /* no data */
        head->right = head;  /* right link points to head node */
        head->rightflag = link;
        *s = head;
        z->left = head;
        z->right = head;
    }
    else {  /* if tree is non-empty */
        p = head->left;
        /* traverse till we reach head */
        while (p != head) {
            if (p->data > num) {
                if (p->leftflag != thread)  /* check for a thread */
                    p = p->left;
                else {
                    z->left = p->left;
                    p->left = z;
                    p->leftflag = link;
                    z->rightflag = thread;
                    z->right = p;
                    return;
                }
            }
            else {
                if (p->data < num) {
                    if (p->rightflag != thread)
                        p = p->right;
                    else {
                        z->right = p->right;
                        p->right = z;
                        p->rightflag = link;
                        z->leftflag = thread;
                        z->left = p;
                        return;
                    }
                }
            }
        }
    }
}

/* traverses the threaded binary tree in inorder */
void inorder(struct thtree *root) {
    struct thtree *p;
    p = root->left;
    
    while (p != root) {
        while (p->leftflag == link)
            p = p->left;
        printf("%d\t", p->data);
        while (p->rightflag == thread) {
            p = p->right;
            if (p == root)
                break;
            printf("%d\t", p->data);
        }
        p = p->right;
    }
}
```

### Output:
```
Threaded binary tree:
7  8  9  10  11  12  13  14  15
```

### Explanation

We have used an enumerated data type `boolean` to store information whether the pointer is a thread or a link. If `leftflag`/`rightflag` is a thread it means that the node has no left/right child.

To insert a new node in the threaded BST, the `insert()` function is called. It first checks for an empty tree. If the tree is empty then firstly a head node is created. Then the node being inserted is made its left sub-tree with both links set up as threads. Otherwise, the node is inserted at an appropriate place by traversing the tree such that the BST nature of the tree is maintained.

The threaded binary tree's in-order traversal is different than a normal tree in the sense that we do not have to stack the pointers to nodes visited earlier so as to reach them later. This is avoided by using the threads to ancestors. The procedure to achieve this is as follows:

This procedure begins by first going to the left sub-tree of the head node. Then through a while loop we follow the left pointers until a thread to a predecessor is found. On encountering this thread, we print the data for the leftmost node. Next, through another while loop we follow the thread back up to the ancestor node and print this ancestor node's data. This way we continue to move up till `rightflag` is a thread. When we reach a link, we go to the right child and again follow the same procedure by checking its left sub-tree.

As we follow these steps, we are sometimes likely to reach the head node, and that is the time to stop the traversal.

---

## AVL Trees

We know that height of a BST is the maximum number of edges from leaf node to root node. Note that if we change the order of insertion of nodes in a BST, we may get BSTs of different heights. As a confirmation, you may try creating two BSTs using the insertion order as 30, 40, 10, 50, 20, 5, 35 and 50, 40, 35, 30, 20, 10, 5. In the first case you would get a BST of height 2 and in the second case a BST of height 6.

Also, search time in a BST depends upon its height. Searching is efficient if the heights of both left and right sub-trees of any node are equal. However, frequent insertions and deletions in a BST are likely to make it unbalanced. The efficiency of searching is ideal if the difference between the heights of left and right sub-trees of all the nodes in a BST is at the most one. Such a binary search tree is called a **Balanced BST**. It was invented in the year 1962 by two Russian mathematicians—G.M. Adelson-Velskii and E.M. Landis. Hence such trees are also known as **AVL trees**. Figure 7-15 shows some examples of AVL trees.

![Figure 7-15: AVL trees](image-placeholder)

The **balance factor** of a node is calculated as height of the left sub-tree minus height of the right sub-tree of the node. The balance factor of any node in an AVL BST should be -1, 0 or 1. If it is other than these three values then the tree is not balanced.

To re-balance and make it an AVL tree the nodes need to be properly adjusted. This is done by doing one of the 4 types of rotations—**Left rotation, Right rotation, Left Right rotation** and **Right Left rotation**. Of these, first two involve a 1 step process, whereas the next two involve a 2-step process.

Figure 7-16 shows LL, RR, LR and RL imbalances and how to correct them by doing appropriate rotations.

![Figure 7-16: LL, RR, LR and RL imbalances and rotations](image-placeholder)

In general, on inserting a new node in an AVL BST we should carry out the following steps:

**Step 1**: Calculate balance factors of all nodes  
**Step 2**: Identify type of imbalance  
**Step 3**: Perform rotation(s)

Let me explain the imbalances and the rotations with the help of cases shown in Figure 7-16. Let us take the first case. Assume that BST already contains nodes 30 and 20. When we insert node 10, it is inserted to the left of 30 and to the left of 20. Now calculate the balance factors. They turn out to be 2, 1 and 0 for nodes 30, 20 and 10 respectively. Out of these, balance factor 2 is unacceptable. Since this was caused by inserting 10 to the left of 30 and to the left of 20, this imbalance is called **LL imbalance**. To correct it, we need to do **right rotation** about 30. Imagine as if there is string attached to node 30 and we are pulling it to the right. The resultant BST has balance factors 0, 0 and 0. Thus the tree is now balanced. On similar lines RR imbalance and the left rotation can be explained.

In the third case when we insert 20 it is inserted to the left of 30 and to the right of 20. Balance factors turn out to be 2, -1 and 0 for nodes 30, 10 and 20 respectively. To correct the imbalance, we need to perform a **left rotation** around 10. The resultant BST has balance factors of 2, 1 and 0. To correct the imbalance we should now perform a **right rotation** around 30. The resultant BST has satisfactory balance factors. On similar lines the RL imbalance can be explained.

In all the four cases discussed above there was only one node that caused the imbalance. In some other case if 2 nodes are unbalanced then we need to rotate about the first ancestor that caused imbalance.

---

## Binary Heap

Binary heap is a **complete binary tree**. It means all its levels are completely filled except perhaps last and at the last level nodes are as much to left as possible.

There are two types of heaps. If the value present at any node is greater than all its children then such a tree is called as the **max heap** or descending heap. In case of a **min heap** or ascending heap the value present in any node is smaller than all its children. Figure 7-17 shows these two types of heaps.

![Figure 7-17: Types of heaps](image-placeholder)

One of the common operations carried out while using a binary heap is **heapification** of a node. While heapifying a node in a max heap, we need to ensure that all its children satisfy the heap property—**Parent >= Left child, Right child**. This operation involves following steps:

(a) Pick maximum out of given node, and its left and right child  
(b) If maximum is root, do nothing  
(c) If maximum is left, exchange root with left and heapify left node  
(d) If maximum is right, exchange root with right and heapify right node

These operations are shown in Figure 7-18.

![Figure 7-18: Heapify operation](image-placeholder)

Note that in the binary tree shown in Figure 7-18 node 13 and node 9 were violating the heap property. While heapifying 13, maximum out of 13, 1, and 90 is 90. Since 90 is the right child, it is exchanged with 13. As against this, while heapifying 9, maximum (25) turns out to be the left child. So 25 is exchanged with 9. Since after exchange 13 and 9 became child nodes, we did not have to heapify them further.

Figure 7-19 shows a case where further heapification is necessary.

![Figure 7-19: Multi-step heapify operation](image-placeholder)

---

### Program 7-3: Construction of max heap

```c
#include <stdio.h>

void heapify(int [], int, int);

int main() {
    int arr[] = {11, 2, 9, 13, 3, 25, 17, 1, 90, 57};
    int i, size;
    
    size = 10;
    
    for (i = size / 2 - 1; i >= 0; i--)
        heapify(arr, size, i);
    
    for (i = 0; i < size; i++)
        printf("%d\t", arr[i]);
}

void heapify(int arr[], int sz, int i) {
    int largest, lch, rch, t;
    
    lch = 2 * i + 1;
    rch = 2 * i + 2;
    
    if (lch >= sz)
        return;
    
    largest = i;
    
    /* if left child is larger than root */
    if (lch < sz && arr[lch] > arr[largest])
        largest = lch;
    
    /* if right child is larger than largest so far */
    if (rch < sz && arr[rch] > arr[largest])
        largest = rch;
    
    /* if largest is not root */
    if (largest != i) {
        t = arr[i];
        arr[i] = arr[largest];
        arr[largest] = t;
        /* heapify the affected sub-tree */
        heapify(arr, sz, largest);
    }
}
```

### Output:
```
90  57  25  13  11  9  17  1  2  3
```

On execution of the program the binary tree shown in Figure 7-20(a) gets converted into a max heap shown in Figure 7-20(b).

![Figure 7-20: Conversion of binary tree to max heap](image-placeholder)

The program begins by declaring an array that represents the binary tree. We know that in array representation of a binary tree, a node at location i has its left and right child at locations (2i+1) and (2i+2) respectively. Next, in the for loop we have repeatedly called `heapify()` moving level by level from leaf towards root, and at any level from right to left, starting from node at location `size/2 - 1`. The `heapify()` function finds the largest out of given node, and its left and right child.

If the given node turns out to be largest then it does nothing. But if left/right child turns out to be largest it exchanges the given node with left/right child and then proceeds to heapify the left/right child.

### Applications of Binary Heap

Binary heap is used in many areas of computer science. Some of these are listed below.

(a) Finding minimum spanning tree  
(b) Finding the shortest path in a network of cities  
(c) Implementing priority queues  
(d) Merging K sorted arrays

---

# Chapter Bullets: Summary of chapter

- (a) Tree is a non-linear data structure.
- (b) Each node in a binary tree can have 0, 1 or 2 children.
- (c) Unlike trees in nature a binary tree has root at the top and leaves at the bottom with root node at level 0.
- (d) Depth of a node is largest number of links from root to that node.
- (e) Height of a node is largest number of links from leaf node to that node.
- (f) A binary tree can be traversed in in-order, pre-order and post-order fashion
- (g) If we know any two sequences out of in-order, pre-order and postorder, it is possible to construct the binary tree.
- (h) A binary tree can be represented using array representation or linked representation.
- (i) BST and AVL trees are special types of binary trees. They are created with an aim to improve the efficiency of working with binary trees.
- (j) The property parent >= child is satisfied for all nodes in a max heap, and parent <= child for all nodes in a min heap.

---

# Check Your Progress

## Exercise - Level I

### [A] State whether the following statements are True or False:

(a) A binary tree whose non-leaf nodes have left and the right child is a complete binary tree.

(b) The number of nodes attached to a particular node in a tree is called the degree of the node.

(c) To reconstruct a unique binary tree the in-order and pre-order lists are required.

(d) The balance factor of a node in an AVL tree is 1 if the height of the left sub-tree is one less than the height of the right sub-tree.

### [B] Fill in the blanks:

(a) In a threaded binary tree, the address of the in-order predecessor and in-order successor are stored in _____ and _____ child of the leaf node respectively.

(b) In any node of B-tree of order n the minimum required values and children are _____ and _____ respectively.

(c) In a heap if the largest element is present at the root node then it is called as the _____

---

## Sharpen Your Skills: Exercise - Level II

### [C] Answer the Following:

(a) Write a program that finds the height of a binary tree.

(b) Write a program that counts the number of nodes in a binary tree and the number of leaf nodes in a binary tree.

(c) Given a binary tree, create another binary tree that is mirror image of the given tree.

(d) Write a program that implements the non-recursive form of the functions `inorder()`, `preorder()` and `postorder()`

---

## Coding Interview Questions: Exercise Level III

### [D] Answer the Following:

(a) Given any number, write a program to find whether that number is present in the binary tree. If present then find the level at which it is present.

(b) Given two binary trees, write a program that finds whether:
- the two binary trees are similar
- the two binary trees are mirror images of each other

(c) Write a program that finds the number of nodes in a binary tree at each level.

(d) Write a program that traverses a binary tree level by level, from left towards right.

(e) Write a function to insert a node t as a left child of any node s in a threaded binary tree.

---

## Case Scenario Exercise: Dictionary implementation

We wish to maintain a dictionary of words as a binary tree. Each node should contain a word, its meaning, a synonym and an antonym. There must be a provision to insert a word, search a word and delete a word. It should be also possible to print the entire dictionary in alphabetical order.
```