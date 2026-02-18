---
title: Data Structures Through C
weight: 2
---

Data Structure is a way of organizing data in such a way that we can perform operations on the data in an effective way. Same data can be stored in different data structures. Each data structure has its own benefits and limitations. A data structure is not related with any specific language. All data structures can be implemented through languages like C, C++, Java, C#, Python, etc. In this book we would be using C language to implement various data structures.

Data structures are classified into two categories—**linear** and **nonlinear**. The elements in a linear data structure form a sequence, whereas elements in a nonlinear data structure do not.

There are two ways of representing linear data structures in memory—**Array based lists** (simply called arrays) and **Linked Lists**. In array the linear relationship between elements is established by storing its elements in sequential memory locations. In linked list the linear relationship is established through pointers or links. In a linked list each node contains the data and the address of the next node. Figure 2-1(a) and Figure 2-1(b) show the representation of an array and a linked list.

**Figure 2-1. Array and Linked list.**

```
(a) Array of 6 integers:
[34] [1] [5] [-6] [12] [9]

(b) Linked list of 4 integers:
[34|*]-->[5|*]-->[1|*]-->[6|N]
  ↑Data  ↑Pointer to next Node
```

Arrays are useful when the number of elements to be stored is fixed. They are easy to traverse, search and sort. On the other hand, linked lists are useful when number of data items in the collection is likely to vary. Linked lists are difficult to maintain as compared to an array. We would discuss linked lists in more detail in Chapter 3.

---