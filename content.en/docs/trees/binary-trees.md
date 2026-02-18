---
title: Binary Trees
weight: 2
---

Let us begin our study of binary trees by discussing some basic concepts and terminology.

A **binary tree** is a finite set of elements that is either empty or is partitioned into three disjoint sub-sets. The first sub-set contains a single element called the **root** of the tree. The other two sub-sets are themselves binary trees, called the **left and right sub-trees** of the original tree. A left or right sub-tree can be empty.

Each element of a binary tree is called a **node** of the tree. The tree shown in Figure 7-2(a) consists of nine nodes with A as its root. Its left sub-tree is rooted at B and its right sub-tree is rooted at C. This is indicated by the two branches emanating from A to B on the left and to C on the right. The absence of a branch indicates an empty sub-tree. For example, the left sub-tree of the binary tree rooted at C and the right sub-tree of the binary tree rooted at E are both empty. The binary trees rooted at D, G, H and I have empty right and left sub-trees.

Figure 7-2(b) illustrates a structure that is **not** a binary tree.

![Figure 7-2: Binary tree](image-placeholder)

### Terminology

| Term | Definition |
|------|------------|
| **Parent, Child** | If A is the root of a binary tree and B is the root of its left or right sub-tree then, A is parent of B and B is left or right child of A. |
| **Leaf** | A node that has no children (such as D, G, H, or I in Figure 7-2(a)) is called a leaf. |
| **Ancestor, Descendant** | Any node n1 is an ancestor of node n2 (and n2 is a descendant of n1) if n1 is either the parent of n2 or the parent of some ancestor of n2. For example, in the tree shown in Figure 7-2(a), A is an ancestor of C. |
| **Climbing, Descending** | The root of the tree is at the top and the leaves at the bottom. Going from the leaves to the root is called climbing the tree, and going from the root to the leaves is called descending the tree. |
| **Degree of a node** | The number of nodes connected to a particular node is called the degree of a particular node. For example, in Figure 7-2(a) the node B has a degree 3. The degree of a leaf node is always one. |
| **Level** | The root of the tree has level 0. Level of any other node in the tree is one more than the level of its parent. For example, in the binary tree shown in Figure 7-2(a), node E is at level 2 and node H is at level 3. |
| **Depth** | Depth of a node is the maximum number of links from root to that node. The depth of a binary tree is the maximum level of any leaf in the tree. This equals the length of the longest path from the root to any leaf. Thus, the depth of the tree shown in Figure 7-2(a) is 3. |
| **Height** | Height of a node is the maximum number of links from that node to leaf node. Height of a binary tree is height of its root node. |

### Types of Binary Trees

**Strictly binary tree**: If every non-leaf node in a binary tree has nonempty left and right sub-trees, the tree is termed a strictly binary tree. Thus, the tree shown in Figure 7-3(a) is a strictly binary tree.

**Complete binary tree**: A complete binary tree (refer Figure 7-3(b)) has maximum number of possible nodes at all levels except the last level, and all the nodes of the last level appear as far left as possible.

![Figure 7-3: Strictly and Complete binary tree](image-placeholder)

---