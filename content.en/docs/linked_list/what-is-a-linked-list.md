---
title: What is a Linked List?
weight: 2
---

While the elements of an array occupy contiguous memory locations, those of a linked list are not constrained to be stored in adjacent locations. The order of the elements is maintained by explicit links between them. For instance, the marks obtained by different students can be stored in a linked list as shown in Figure 3-1.

![Figure 3-1: Linked list](image-placeholder)

Observe that the linked list is a collection of elements called **nodes**, each of which stores two items of information—an element of the list and a link. In Figure 3-1, the data part of each node consists of the marks obtained by a student and the link part contains address of the next node. Thus, the link part is a pointer to the next node. Hence it is shown using an arrow. The NULL (N) in the last node indicates that it is the last node in the list.

---