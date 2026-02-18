---
title: Binary Tree Sort
weight: 12
---

Binary tree sort uses a binary search tree (BST). In this algorithm, each element in the input list is inserted in a BST. During insertion the element being inserted is compared with nodes in the BST starting with the root node and moving towards the leaf nodes. If the element is less than node, then it is placed in the left branch, otherwise in the right branch. After all elements are inserted in the BST, it is traversed in inorder (left, root, right) to get the elements in ascending order.

Let's understand this in more details. Suppose `arr` is an array that consists of 10 distinct elements. The elements are as follows:
```
11, 2, 9, 13, 57, 25, 17, 1, 90, 3
```

The BST that can be built from these elements is shown in Figure 9-7.

**Figure 9-7: Binary Tree sort at work**

```
                    11
                   /  \
                  2    13
                 / \     \
                1   9     57
                   /     /  \
                  3     25   90
                       /
                      17

Input list: 11, 2, 9, 13, 57, 25, 17, 1, 90, 3

In-order traversal: 1, 2, 3, 9, 11, 13, 17, 25, 57, 90
```

The binary tree sort algorithm works as follows:

(a) To construct the binary search tree, we start with the 0th element 11. It is made the root of the tree.

(b) While inserting the 1st element, i.e., 2, 2 is compared with the root node 11. Since 2 is less than 11 it is made the left child of the root node 11.

(c) While inserting the 2nd element of the list, i.e., 13, it is compared with the root element 11. Since 13 is greater than 11 it is made the right child of the root node 11.

(d) Similarly, all other elements are placed in their proper position in the binary search tree.

(e) Now to get the elements in the sorted order, the tree is traversed in in-order and the elements are restored in the array.

The following program implements the binary tree sort algorithm.

### Program 9-8: Implementation of Binary Tree Sort algorithm

```c
#include <stdio.h>
#include <stdlib.h>

struct btreenode {
    struct btreenode *leftchild;
    int data;
    struct btreenode *rightchild;
};

void binarytreesort(int [], int);
void insert(struct btreenode **, int);
void inorder(struct btreenode *, int [], int *);

int main() {
    int arr[] = {11, 2, 9, 13, 57, 25, 17, 1, 90, 3};
    int i;
    
    printf("Binary Tree sort\n");
    printf("Array before sorting:\n");
    for (i = 0; i < 10; i++)
        printf("%d\t", arr[i]);
    
    binarytreesort(arr, 10);
    
    printf("\nArray after sorting:\n");
    for (i = 0; i < 10; i++)
        printf("%d\t", arr[i]);
    
    return 0;
}

void binarytreesort(int a[], int size) {
    struct btreenode *bt;
    int i;
    bt = NULL;
    for (i = 0; i < size; i++)
        insert(&bt, a[i]);
    i = 0;
    inorder(bt, a, &i);
}

void insert(struct btreenode **pr, int num) {
    if (*pr == NULL) {
        *pr = (struct btreenode *)malloc(sizeof(struct btreenode));
        (*pr)->leftchild = NULL;
        (*pr)->data = num;
        (*pr)->rightchild = NULL;
    }
    else {
        if (num < (*pr)->data)
            insert(&((*pr)->leftchild), num);
        else
            insert(&((*pr)->rightchild), num);
    }
}

void inorder(struct btreenode *pr, int a[], int *p) {
    if (pr != NULL) {
        inorder(pr->leftchild, a, p);
        a[*p] = pr->data;
        *p = *p + 1;
        inorder(pr->rightchild, a, p);
    }
}
```

### Output:
```
Binary Tree sort
Array before sorting:
11	2	9	13	57	25	17	1	90	3	
Array after sorting:
1	2	3	9	11	13	17	25	57	90	
```

The `binarytreesort()` function calls `insert()` function for each element in the array to construct the BST, and `inorder()` function to visit the constructed BST in in-order fashion.

In the `insert()` function it is ascertained whether BST is empty or not. If it is empty then a new node is created and the data to be inserted is stored in it. The left and right child of this new node is set with a NULL value, as this is the first node being inserted.

If BST is not empty then the current node is compared with the data to be inserted and `insert()` function is called recursively to insert the node in the left/right sub-tree. Thus `insert()` continues to move down the levels of BST until it reaches a leaf node. When it does, the new node gets inserted in the left/right sub-tree.

The `inorder()` function receives address of the root node of BST, address of the array and an index where each visited element of BST should be inserted in the array. In the function a condition is checked whether the pointer is NULL. If the pointer is not NULL then a recursive call is made first for the left child and then for the right child. The values passed are the address of the left and right children that are present in the pointers `leftchild` and `rightchild` respectively. In between these two calls the data of the current node is stored in the array.

In binary tree sort there are two distinct steps—creation of BST and visiting it in in-order. The worst case will be if the array is already in sorted order. Let us discuss the time complexity in this case.

While constructing the BST, to insert 1st element of this array into BST we have to perform 1 comparison, to insert 2nd element we have to do 2 comparisons, to insert 3rd element we have to do 3 comparisons. So to insert n elements it has to do n(n+1)/2 comparisons.

If there are n elements in the list there will be n nodes in the BST. While performing in-order traversal of the BST we perform maximum of 3 comparisons for any node. For n nodes the maximum number of comparisons will be 3n.

So, total number of comparisons for this algorithm will be n(n+1)/2 + 3n. Ignoring constants and lower order terms, time complexity of binary tree sort will be **O(n²)**.

The drawback of the binary tree sort is that additional space is required for building the BST.

---