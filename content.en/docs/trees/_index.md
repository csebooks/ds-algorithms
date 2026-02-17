---
title: 'Trees'
weight: 4
references:
    books:
        - b1:
            title: Data Structures and Algorithm Analysis in C by Mark Allen Weiss 
            url: https://mrajacse.files.wordpress.com/2012/08/data-structures-and-algorithm-analysis-in-c-mark-allen-weiss.pdf
        - b2:
            title: Data_Structures_and_Algorithm_Analysis_2e By mark-allen-weiss
            url: https://www.google.co.in/books/edition/Data_Structures_and_Algorithm_Analysis_i/83RWbPynhkgC?hl=en&gbpv=1
    links:
        - https://visualgo.net/en/bst?slide=1
---

## Trees

For large amounts of input, the linear access time of linked lists is prohibitive. In this chapter we look at a simple data structure for which the running time of most operations is O(log n) on average. We also sketch a conceptually simple modification to this data structure that guarantees the above time bound in the worst case and discuss a second modification that essentially gives an O(log n) running time per operation for a long sequence of instructions.

The data structure that we are referring to is known as a binary search tree. Trees in general are very useful abstractions in computer science, so we will discuss their use in other, more general applications. In this chapter, we will

- See how trees are used to implement the file system of several popular operating systems.

- See how trees can be used to evaluate arithmetic expressions.

- Show how to use trees to support searching operations in O(log n) average time, and how to refine these ideas to obtain O(log n) worst-case bounds. We will also see how to implement these operations when the data is stored on a disk.
