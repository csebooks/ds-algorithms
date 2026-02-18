---
title: AVL Trees
weight: 8
---

We know that height of a BST is the maximum number of edges from leaf node to root node. Note that if we change the order of insertion of nodes in a BST, we may get BSTs of different heights. Also, search time in a BST depends upon its height. Searching is efficient if the heights of both left and right sub-trees of any node are equal. However, frequent insertions and deletions in a BST are likely to make it unbalanced.

The efficiency of searching is ideal if the difference between the heights of left and right sub-trees of all the nodes in a BST is at the most one. Such a binary search tree is called a **Balanced BST**. It was invented in the year 1962 by two Russian mathematicians—**G.M. Adelson-Velskii and E.M. Landis**. Hence such trees are also known as **AVL trees**.

![Figure 7-15: AVL trees](image-placeholder)

The **balance factor** of a node is calculated as:
> **Balance Factor = height of left sub-tree - height of right sub-tree**

The balance factor of any node in an AVL BST should be **-1, 0, or 1**. If it is other than these three values then the tree is not balanced.

To re-balance and make it an AVL tree the nodes need to be properly adjusted. This is done by doing one of the **4 types of rotations**:

| Rotation | Type | Process |
|----------|------|---------|
| **Left rotation** | 1-step | For RR imbalance |
| **Right rotation** | 1-step | For LL imbalance |
| **Left-Right rotation** | 2-step | For LR imbalance |
| **Right-Left rotation** | 2-step | For RL imbalance |

![Figure 7-16: LL, RR, LR and RL imbalances and rotations](image-placeholder)

### Steps for Insertion in AVL BST:

1. **Step 1**: Calculate balance factors of all nodes
2. **Step 2**: Identify type of imbalance
3. **Step 3**: Perform rotation(s)

---