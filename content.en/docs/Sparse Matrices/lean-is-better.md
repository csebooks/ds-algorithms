---
title: Lean Is Better
weight: 1
---

### Why This Chapter Matters?

Computer's memory is a costly resource. We have to use it judiciously. Sparse matrices often eat away lot of costly memory space. This chapter explains how to conserve this memory and still work with matrices efficiently.

---

71 percent of earth is occupied by water, leaving a meagerly 29 percent for land. It is only natural that we need to conserve the available space. Nobody should occupy more space than what they deserve to occupy, be it animals, man, plants or matrices. There is no point in wasting costly space in computer's memory in storing elements that do not deserve a place in it. Sparse matrix is the case in point.

If many elements from a matrix have a value 0 then the matrix is known as a **sparse matrix**. There is no precise definition of when a matrix is sparse and when it is not, but it is a concept, which we can all recognize intuitively. If the matrix is sparse, we must consider an alternate way of representing it rather than the normal row major or column major arrangement. This is because if majority of elements of the matrix are 0 then an alternative through which we can store only the non-zero elements and keep intact the functionality of the matrix can save a lot of memory space. Figure 4-1 shows a sparse matrix of dimension 7×7.

**Figure 4-1: Representation of a sparse matrix of dimension 7 x 7**

```
Columns
    0   1   2   3   4   5   6
   ┌───┬───┬───┬───┬───┬───┬───┐
0  │ 0 │ 0 │ 0 │-5 │ 0 │ 0 │ 0 │
   ├───┼───┼───┼───┼───┼───┼───┤
1  │ 0 │ 4 │ 0 │ 0 │ 0 │ 0 │ 7 │
   ├───┼───┼───┼───┼───┼───┼───┤
2  │ 0 │ 0 │ 0 │ 0 │ 9 │ 0 │ 0 │
   ├───┼───┼───┼───┼───┼───┼───┤
3  │ 0 │ 3 │ 0 │ 2 │ 0 │ 0 │ 0 │
   ├───┼───┼───┼───┼───┼───┼───┤
4  │ 1 │ 0 │ 2 │ 0 │ 0 │ 0 │ 0 │
   ├───┼───┼───┼───┼───┼───┼───┤
5  │ 0 │ 0 │ 0 │ 0 │ 0 │ 0 │ 0 │
   ├───┼───┼───┼───┼───┼───┼───┤
6  │ 0 │ 0 │ 8 │ 0 │ 0 │ 0 │ 0 │
   └───┴───┴───┴───┴───┴───┴───┘
Rows
```

A common way of representing non-zero elements of a sparse matrix is the **3-tuple form**. In this form each non-zero element is stored in a row, with the 1st and 2nd element of this row containing the row and column in which the element is present in the original matrix. The 3rd element in this row stores the actual value of the non-zero element. For example, the 3-tuple representation of the sparse matrix shown in Figure 4-1 is given below.

```c
int spmat[10][3] = {
    7, 7, 9,      // Total rows, total columns, total non-zero elements
    0, 3, -5,     // row 0, col 3, value -5
    1, 1, 4,      // row 1, col 1, value 4
    1, 6, 7,      // row 1, col 6, value 7
    2, 4, 9,      // row 2, col 4, value 9
    3, 1, 3,      // row 3, col 1, value 3
    3, 3, 2,      // row 3, col 3, value 2
    4, 0, 1,      // row 4, col 0, value 1
    4, 2, 2,      // row 4, col 2, value 2
    6, 2, 8       // row 6, col 2, value 8
};
```

There are two ways in which information of a 3-tuple can be stored:
- Arrays
- Linked List

In both representations information about the non-zero elements is stored. However, as the number of non-zero elements in a sparse matrix may vary, it would be efficient to use a linked list to represent it.

---