---
title: 'Tree Traversals'
weight: 6
references:
    books:
        - b1:
            title: Data Structures and Algorithm Analysis in C by Mark Allen Weiss 
            url: https://mrajacse.files.wordpress.com/2012/08/data-structures-and-algorithm-analysis-in-c-mark-allen-weiss.pdf
        - b2:
            title: Data_Structures_and_Algorithm_Analysis_2e By mark-allen-weiss
            url: https://www.google.co.in/books/edition/Data_Structures_and_Algorithm_Analysis_i/83RWbPynhkgC?hl=en&gbpv=1
---


## Tree Traversals (Revisited)

Because of the ordering information in a binary search tree, it is simple to list all the keys in sorted order. The recursive procedure in Figure 4.60 does this.

Convince yourself that this procedure works. As we have seen before, this kind of routine when applied to trees is known as an inorder traversal (which makes sense, since it lists the keys in order). The general strategy of an inorder traversal is to process the left subtree first, then perform processing at the current node, and finally process the right subtree. The interesting part about this algorithm, aside from its simplicity, is that the total running time is O (n). This is because there is constant work being performed at every node in the tree. Each node is visited once, and the work performed at each node is testing against NULL, setting up two procedure calls, and doing a print_element. Since there is constant work per node and n nodes, the running time is O(n).
```c
void print_tree(SEARCH_TREE T)
{

if(T != NULL){print_tree(T->left);

print_element(T->element);

print_tree(T->right);

}

}
```
**Figure 4.60 Routine to print a binary search tree in order**

Sometimes we need to process both subtrees first before we can process a node. For instance, to compute the height of a node, we need to know the height of the subtrees first. The code in Figure 4.61 computes this. Since it is always a good idea to check the special cases - and crucial when recursion is involved - notice that the routine will declare the height of a leaf to be zero, which is correct. This general order of traversal, which we have also seen before, is known as a postorder traversal. Again, the total running time is O(n), because constant work is performed at each node.

The third popular traversal scheme that we have seen is preorder traversal. Here, the node is processed before the children. This could be useful, for example, if you wanted to label each node with its depth.

The common idea in all of these routines is that you handle the NULL case first, and then the rest. Notice the lack of extraneous variables. These routines pass only the tree, and do not declare or pass any extra variables. The more compact the code, the less likely that a silly bug will turn up. A fourth, less often used, traversal (which we have not seen yet) is level-order traversal. In a level-order traveresal, all nodes at depth d are processed before any node at depth d + 1. Level-order traversal differs from the other traversals in that it is not done recursively; a queue is used, instead of the implied stack of recursion.
```
int

height(TREE T)
{

if(T == NULL)
return -1;

else
return (max(height(T->left), height(T->right)) + 1);

}
```
**Figure 4.61 Routine to compute the height of a tree using a postorder traversal**
