---
title: 'Hashing'
weight: 5
references:
    books:
        - b1:
            title: Data Structures and Algorithm Analysis in C by Mark Allen Weiss 
            url: https://mrajacse.files.wordpress.com/2012/08/data-structures-and-algorithm-analysis-in-c-mark-allen-weiss.pdf
        - b2:
            title: Data_Structures_and_Algorithm_Analysis_2e By mark-allen-weiss
            url: https://www.google.co.in/books/edition/Data_Structures_and_Algorithm_Analysis_i/83RWbPynhkgC?hl=en&gbpv=1
    links:
        - https://visualgo.net/en/hashtable?slide=1
---

# Hashing

In Previous Chapter, we discussed the search tree ADT, which allowed various operations on a set of elements. In this chapter, we discuss the hash table ADT, which supports only a subset of the operations allowed by binary search trees.

The implementation of hash tables is frequently called hashing. Hashing is a technique used for performing insertions, deletions and finds in constant average time. Tree operations that require any ordering information among the elements are not supported efficiently. Thus, operations such as find_min, find_max, and the printing of the entire table in sorted order in linear time are not supported.

- The central data structure in this chapter is the hash table. We will See several methods of implementing the hash table.

- Compare these methods analytically.

- Show numerous applications of hashing.

- Compare hash tables with binary search trees.
