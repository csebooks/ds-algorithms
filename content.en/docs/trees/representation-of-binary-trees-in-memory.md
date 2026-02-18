---
title: Representation of Binary Trees in Memory
weight: 3
---

There are two ways by which we can represent a binary tree—**Linked representation** and **Array representation**.

### Linked Representation of Binary Trees

In linked representation each node contains addresses of its left child and right child. If a child is absent, the link contains a NULL value. For example, in Figure 7-4 the link fields of node C contain the address of the nodes F and G. The left link field of node E contains the address of the node H. Similarly, the right link contains a NULL as E has no right child. The nodes D, F, G and H contain a NULL value in both their link fields, as these are the leaf nodes.

![Figure 7-4: Linked representation of a Binary tree](image-placeholder)

### Array Representation of Binary Trees

When a binary tree is represented by arrays three separate arrays are required. One array `arr` stores the data fields of the trees. The other two arrays `lc` and `rc` represents the left child and right child of the nodes. Figure 7-5 shows these three arrays, which represents the tree shown in Figure 7-4.

![Figure 7-5: Array representation of a binary tree](image-placeholder)

The arrays `lc` and `rc` contains the index of the array `arr` where the data is present. If the node does not have any left child or right child then the element of the array `lc` or `rc` contains a value -1. The 0th element of the array `arr` contains the root node data. Some elements of the array `arr` contain `'\0'` which represents an empty child.

Suppose we wish to find the left and right child of the node E. Then we need to find the value present at index 4 in array `lc` and `rc` since E is present at index 4 in the array `arr`. The value present at index 4 in the array `lc` is 9, which is the index position of node H in the array `arr`. So, the left child of the node E is H. The right child of the node E is empty because the value present at index 4 in the array `rc` is –1.

We can also represent a binary tree using **one single array**. For this, numbers are given to each node starting from the root node—0 to root node, 1 to the left node of the first level, then 2 to the second node from left of the first level and so on. In other words, the nodes are numbered from left to right level by level from top to bottom. Figure 7-6(a) shows the numbers given to each node in the tree. Note that while numbering the nodes of the tree, empty nodes are also taken into account.

![Figure 7-6: Array representation of binary tree using one array](image-placeholder)

It can be observed that if n is the number given to the node, then its left child is at position **(2n+1)** in the array and right child at position **(2n+2)**. If any node doesn't have a left or a right child then an empty node is assumed and a value `'\0'` is stored at that index in the array.

---