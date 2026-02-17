---
title: 'Simple Implementations'
weight: 2
---

## Simple Implementations

There are several obvious ways to implement a priority queue. We could use a simple linked list, performing insertions at the front in O(1) and traversing the list, which requires O(n) time, to delete the minimum. Alternatively, we could insist that the list be always kept sorted; this makes insertions expensive (O (n)) and delete_mins cheap (O(1)). The former is probably the better idea of the two, based on the fact that there are never more delete_mins than insertions.

Another way of implementing priority queues would be to use a binary search tree. This gives an O(log n) average running time for both operations. This is true in spite of the fact that although the insertions are random, the deletions are not. Recall that the only element we ever delete is the minimum. Repeatedly removing a node that is in the left subtree would seem to hurt the balance of the tree by making the right subtree heavy. However, the right subtree is random. In the worst case, where the delete_mins have depleted the left subtree, the right subtree would have at most twice as many elements as it should. This adds only a small constant to its expected depth. Notice that the bound can be made into a worst-case bound by using a balanced tree; this protects one against bad insertion sequences.

Using a search tree could be overkill because it supports a host of operations that are not required. The basic data structure we will use will not require pointers and will support both operations in O(log n) worst-case time. Insertion will actually take constant time on average, and our implementation will allow building a heap of n items in linear time, if no deletions intervene. We will then discuss how to implement heaps to support efficient merging. This additional operation seems to complicate matters a bit and apparently requires the use of pointers.
