---
title: Two-Dimensional Arrays
weight: 4
---

A 2-dimensional array is a collection of elements placed in m rows and n columns. The syntax used to declare a 2-D array includes two subscripts, of which one specifies the number of rows and the other specifies the number of columns of an array. These two subscripts are used to reference an element in an array. For example, `arr[3][4]` is a 2-D array containing 3 rows and 4 columns and `arr[0][2]` is an element placed at 0th row and 2nd column in the array. The two-dimensional array is also called a **matrix**.

**Figure 2-3. Representation of a 2-D array.**

```
        COLUMN
        0    1    2    3
    +----+----+----+----+
  0 | 12 |  1 | -9 | 23 |
ROW +----+----+----+----+
  1 | 14 |  7 | 11 |121 |
    +----+----+----+----+
  2 |  6 | 78 | 15 | 34 |
    +----+----+----+----+
```

### Row Major and Column Major Arrangement

Rows and columns of a matrix are only a matter of imagination. When a matrix gets stored in memory all its elements are stored linearly since computer's memory can only be viewed as consecutive units of memory locations. This leads to two possible arrangements of elements in memory: **Row Major Arrangement** and **Column Major Arrangement**. Figure 2-4 illustrates these two possible arrangements for a 2-D array.

**Figure 2-4. Possible arrangements of 2-D array.**

```c
int a[3][4] = {
    { 12, 1, -9, 23 },
    { 14, 7, 11, 121 },
    { 6, 78, 15, 34 }
};
```

**Row Major Arrangement:**
```
Addresses: 502   506   510   514   518   522   526   530   534   538   542   546
           +----+----+----+----+----+----+----+----+----+----+----+----+
           | 12 |  1 | -9 | 23 | 14 |  7 | 11 |121 |  6 | 78 | 15 | 34 |
           +----+----+----+----+----+----+----+----+----+----+----+----+
           |<--- 0th row --->|<--- 1st row --->|<--- 2nd row --->|
```

**Column Major Arrangement:**
```
Addresses: 502   506   510   514   518   522   526   530   534   538   542   546
           +----+----+----+----+----+----+----+----+----+----+----+----+
           | 12 | 14 |  6 |  1 |  7 | 78 | -9 | 11 | 15 | 23 |121 | 34 |
           +----+----+----+----+----+----+----+----+----+----+----+----+
           |<--- 0th col --->|<--- 1st col --->|<--- 2nd col --->|<-3rd->|
```

*Note: Each integer occupies four-bytes*

Since the array elements are stored in adjacent memory locations, we can access any element of the array once we know the base address (starting address) of the array and number of rows and columns present in the array.

For example, if the base address of the array shown in Figure 2-4 is 502 and we wish to refer the element 121, then the calculation involved would be as follows:

#### Row Major Arrangement

Element 121 is present at `a[1][3]`. Hence location of 121 would be:
```
= 502 + 1 * 4 + 3 = 502 + 7 = 530
```

In general, for an array `a[m][n]` the address of element `a[i][j]` would be:
```
Base address + i * n + j
```

#### Column Major Arrangement

Element 121 is present at `a[1][3]`. Hence location of 121 would be:
```
= 502 + 3 * 3 + 1 = 502 + 10 = 542
```

In general, for an array `a[m][n]` the address of element `a[i][j]` would be:
```
Base address + j * m + i
```

**Note that C language permits only Row Major Arrangement.**

---