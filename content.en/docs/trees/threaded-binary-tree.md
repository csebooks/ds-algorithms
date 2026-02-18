---
title: Threaded Binary Tree
weight: 7
---

In the linked representation of a binary tree, many nodes contain a NULL pointer, either in their left or right fields or in both. Instead of wasting space in storing a NULL pointer, it can be efficiently used to store pointer to the **in-order predecessor** or the **in-order successor** of the node. These special pointers are called **threads** and binary trees containing threads are called **threaded binary trees**.

In threaded binary trees:
- **Right threads**: pointers that point to in-order successor of a node
- **Left threads**: pointers that point to in-order predecessor of a node

The threads are typically denoted using arrows as shown in Figure 7-13.

![Figure 7-13: Threaded binary tree](image-placeholder)

Figure 7-13(b) shows a **head node** containing a value -999. The entire binary tree is shown as the left child of this head node. The right link of the head node points to itself. This head node is useful while creating programs for threaded binary tree. For example, while traversing the tree we can start with head node, visit each node and stop the traversal when we reach the head node once again.

In a program to help us distinguish between a pointer and a thread, the structure that represents a node contains two additional fields, `leftflag` and `rightflag`. If they contain a true, they represent a thread, and if they contain a false, then they represent a pointer to a child node.

```c
struct thtree {
    enum boolean leftflag;
    struct thtree *left;
    int data;
    struct thtree *right;
    enum boolean rightflag;
};
```

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
    th_head = NULL; /* empty tree */
    
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
        head->left = z; /* z becomes leftchild of the head node */
        head->data = -9999; /* no data */
        head->right = head; /* right link points to head node */
        head->rightflag = link;
        *s = head;
        z->left = head;
        z->right = head;
    } else { /* if tree is non-empty */
        p = head->left;
        /* traverse till we reach head */
        while (p != head) {
            if (p->data > num) {
                if (p->leftflag != thread) /* check for a thread */
                    p = p->left;
                else {
                    z->left = p->left;
                    p->left = z;
                    p->leftflag = link;
                    z->rightflag = thread;
                    z->right = p;
                    return;
                }
            } else {
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

**Output:**
```
Threaded binary tree:
7	8	9	10	11	12	13	14	15	
```

---