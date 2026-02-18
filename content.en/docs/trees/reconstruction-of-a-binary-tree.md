---
title: Reconstruction of a Binary Tree
weight: 6
---

If we know the sequence of nodes obtained through in-order/preorder/post-order traversal it may not be feasible to reconstruct the binary tree. This is because two different binary trees may yield same sequence of nodes when traversed using post-order traversal. Similarly, in-order or pre-order traversal of different binary trees may yield the same sequence of nodes.

However, **we can construct a unique binary tree if the results of in-order and pre-order traversal are available.**

**Example:**
- In-order traversal: 4, 7, 2, 8, 5, 1, 6, 9, 3
- Pre-order traversal: 1, 2, 4, 7, 5, 8, 3, 6, 9

We know that the first value in the pre-order traversal gives us the root of the binary tree. So, the node with data **1** becomes the root of the binary tree. In in-order traversal, initially the left sub-tree is traversed then the root node and then the right sub-tree. So, the data before 1 in the in-order list (i.e. 4, 7, 2, 8, 5) forms the left sub-tree and the data after 1 in the in-order list (i.e. 6, 9, 3) forms the right sub-tree.

![Figure 7-12: Reconstruction of a binary tree](image-placeholder)

---