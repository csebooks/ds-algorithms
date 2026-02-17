---
title: 'Amortized Analysis'
weight: 11
references:
    books:
        - b1:
            title: Data Structures and Algorithm Analysis in C by Mark Allen Weiss 
            url: https://mrajacse.files.wordpress.com/2012/08/data-structures-and-algorithm-analysis-in-c-mark-allen-weiss.pdf
        - b2:
            title: Data_Structures_and_Algorithm_Analysis_2e By mark-allen-weiss
            url: https://www.google.co.in/books/edition/Data_Structures_and_Algorithm_Analysis_i/83RWbPynhkgC?hl=en&gbpv=1
---

# Amortized Analysis

In this chapter, we will analyze the running time for several of the advanced data structures that have been presented in Chapters 4 and 6. In particular, we will consider the worst-case running time for any sequence of m operations. This contrasts with the more typical analysis, in which a worst-case bound is given for any single operation.

As an example, we have seen that **AVL** trees support the standard tree operations in O(log n) worst-case time per operation.**AVL** trees are somewhat complicated to implement, not only because there are a host of cases, but also because height balance information must be maintained and updated correctly. The reason that

**AVL** trees are used is that a sequence of (n) operations on an unbalanced

search tree could require (n2) time, which would be expensive. For search trees, the O(n) worst-case running time of an operation is not the real problem. The major problem is that this could happen repeatedly. Splay trees offer a

pleasant alternative. Although any operation can still require (n) time, this degenerate behavior cannot occur repeatedly, and we can prove that any sequence of m operations takes O(m log n) worst-case time (total). Thus, in the long run this data structure behaves as though each operation takes O(log n). We call this an amortized time bound.

Amortized bounds are weaker than the corresponding worst-case bounds, because there is no guarantee for any single operation. Since this is generally not important, we are willing to sacrifice the bound on a single operation, if we can retain the same bound for the sequence of operations and at the same time simplify the data structure. Amortized bounds are stronger than the equivalent average-case bound. For instance, binary search trees have O (log n) average time per operation, but it is still possible for a sequence of m operations to take O (mn) time.

Because deriving an amortized bound requires us to look at an entire sequence of operations instead of just one, we expect that the analysis will be more tricky. We will see that this expectation is generally realized.

In this chapter we shall

- Analyze the binomial queue operations.

- Analyze skew heaps.

- Introduce and analyze the Fibonacci heap.

- Analyze splay trees.
