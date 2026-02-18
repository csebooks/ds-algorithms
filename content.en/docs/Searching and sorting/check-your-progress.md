---
title: Check Your Progress
weight: 16
---

### Exercise - Level I

**[A] State whether the following statements are True or False:**

(a) Sorting is the method of arranging a list of elements in a particular order.

(b) Linear search is more efficient than the binary search.

(c) Merge sort needs additional space to sort an array.

(d) Binary tree sort needs additional space to sort an array.

(e) Time complexity of Quick sort is O(n log₂ n).

(f) Insertion sort is more efficient than Heap sort.

---

### Exercise - Level II

**[B] Answer the Following:**

(a) What is the difference between an internal sorting and external sorting?

(b) Write a program that determines the first occurrence of a given sub-array within an array.

---

### Exercise Level III: Coding Interview Questions

**[C] Answer the Following:**

(a) Suppose an array contains n elements. Given a number x that may occur several times in the array. Find:
   - the number of occurrences of x in the array
   - the position of first occurrence of x in the array.

(b) Write a program that implements insertion sort algorithm for a linked list of integers.

(c) Write a program that sorts the elements of a two-dimensional array row wise / column wise.

---

### Case Scenario Exercise: External Sorting

External sorting is useful for sorting huge amount of data that cannot be accommodated in the memory all at a time. So data from the disk is loaded into memory part by part and each part that is loaded is sorted and the sorted data is stored into some intermediate file. Finally, all the sorted parts present in different intermediate files are merged into one single file.

Initially the original file (file number 1) is partitioned into two files (file number 2 and 3). Then one item is read from each file (file number 2 and 3) and the two items are written in sorted order in a new file (file number 4). Once again one item is read from each partitioned files (file number 2 and 3) and these two items are written in sorted order in another new file (file number 5). Thus, alternate pair of sorted items are stored in the file number 4 and 5. This procedure is repeated till the partitioned files (file number 2 and 3) come to an end.

Now following procedure is repeated twice:

(a) Read one item from file number 4 and 5 and write them in sorted order in file number 2.

(b) Read one item from file number 4 and 5 and write them in sorted order in file number 3.

Note that instead of creating two new files, the partitioned files (2 and 3) are being reused.

After this the following procedure is repeated 4 times:

(a) Read one item from file number 2 and 3 and write them in sorted order in file number 4.

(b) Read one item from file number 2 and 3 and write them in sorted order in file number 5.

In this way alternately items are moved from a pair of partitioned files to the pair of new files and from pair of new files to a pair of partitioned files. This procedure is repeated till the time we do not end up writing entire data in a single file. When this happens all the items in this file would be in sorted order.

Write a program that implements the external sort algorithm.
```