---
title: Multidimensional Arrays
weight: 6
---

A 3-dimensional array can be thought of as an array of arrays of arrays. Figure 2-5 shows a 3-D array, which is a collection of three 2-D arrays each containing 4 rows and 2 columns.

**Figure 2-5. Representation of a 3-D array.**

```
    2nd 2-D Array    1st 2-D Array    0th 2-D Array
         ↓               ↓               ↓
       +-----+         +-----+         +-----+
       | 3 9 |         | 3 2 |         | 2 8 |
       +-----+         +-----+         | 0 6 |
                                       | 4 7 |
                                       | 1 5 |
                                       +-----+
```

This array can be defined as:
```c
int a[3][4][2] = {
    {{2,8}, {0,6}, {4,7}, {1,5}},
    {{3,2}, {8,6}, {1,6}, {4,5}},
    {{3,9}, {1,8}, {6,5}, {4,0}}
};
```

The outer array has three elements, each of which is a 2D array, which in turn holds four 1D arrays containing two integers each. Note that the arrangement shown in Figure 2-5 is only conceptually true. In memory the same array elements are stored linearly as shown in Figure 2-6.

**Figure 2-6. Memory representation of a 3-D array.**

```
Addresses: 402                                              434                                              466
           +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
           |2 |8 |0 |6 |4 |7 |1 |5 |3 |2 |8 |6 |1 |6 |4 |5 |3 |9 |1 |8 |6 |5 |4 |0 |
           +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
           |<------- 0th 2-D array ------->|<------- 1st 2-D array ------->|<------- 2nd 2-D array ------->|
```

As stated earlier, C permits only a Row Major arrangement for multidimensional arrays. Let us determine the location of element 9 in the array shown in Figure 2-6. Element 9 is present at `a[2][0][1]` indicating that it is present in 0th row, 1st column of 2nd 2-D array. Hence address of 9 would be:
```
402 + 2 * 4 * 2 + 0 * 2 + 1 = 402 + 17 = 470
```

For any 3-D array `a[x][y][z]` arranged in Row Major fashion the element `a[i][j][k]` can be accessed using:
```
Base address + i * y * z + j * z + k
```

The formula for Column Major arrangement would be:
```
Base address + i + k * x * y + j * x + i
```

On similar lines for a 4-D array `a[w][x][y][z]` the element `a[i][j][k][l]` can be accessed using following formulae:

- **Row Major:** Base address + i * x * y * z + j * y * z + k * z + l
- **Column Major:** Base address + l * w * x * y + k * w * x + j * w + i

---