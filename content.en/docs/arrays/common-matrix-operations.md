---
title: Common Matrix Operations
weight: 5
---

Common matrix operations are addition, multiplication and transposition. The following program demonstrates these different matrix operations.

### Honest Solid Code
**Program 2-2. Implementation of common matrix operations**

```c
#include <stdio.h>
#define MAX 3

void create(int [3][3]);
void display(int [3][3]);
void matadd(int [3][3], int [3][3], int [3][3]);
void matmul(int [3][3], int [3][3], int [3][3]);
void transpose(int [3][3], int [3][3]);

int main()
{
    int mat1[3][3], mat2[3][3], mat3[3][3], mat4[3][3], mat5[3][3];
    
    printf("Enter elements for first array:\n");
    create(mat1);
    printf("Enter elements for second array:\n");
    create(mat2);
    
    printf("First Array:\n");
    display(mat1);
    printf("Second Array:\n");
    display(mat2);
    
    matadd(mat1, mat2, mat3);
    printf("After Addition:\n");
    display(mat3);
    
    matmul(mat1, mat2, mat4);
    printf("After Multiplication:\n");
    display(mat4);
    
    transpose(mat1, mat5);
    printf("Transpose of first matrix:\n");
    display(mat5);
    
    return 0;
}

/* creates matrix mat */
void create(int mat[3][3])
{
    int i, j;
    for (i = 0; i < MAX; i++)
    {
        for (j = 0; j < MAX; j++)
        {
            printf("Enter the element:");
            scanf("%d", &mat[i][j]);
        }
    }
    printf("\n");
}

/* displays the contents of matrix */
void display(int mat[3][3])
{
    int i, j;
    for (i = 0; i < MAX; i++)
    {
        for (j = 0; j < MAX; j++)
            printf("%d\t", mat[i][j]);
        printf("\n");
    }
}

/* adds two matrices m1 and m2 */
void matadd(int m1[3][3], int m2[3][3], int m3[3][3])
{
    int i, j;
    for (i = 0; i < MAX; i++)
    {
        for (j = 0; j < MAX; j++)
            m3[i][j] = m1[i][j] + m2[i][j];
    }
}

/* multiplies two matrices m1 and m2 */
void matmul(int m1[3][3], int m2[3][3], int m3[3][3])
{
    int i, j, k;
    for (k = 0; k < MAX; k++)
    {
        for (i = 0; i < MAX; i++)
        {
            m3[k][i] = 0;
            for (j = 0; j < MAX; j++)
                m3[k][i] += m1[k][j] * m2[j][i];
        }
    }
}

/* obtains transpose of matrix m1 */
void transpose(int m1[3][3], int m2[3][3])
{
    int i, j;
    for (i = 0; i < MAX; i++)
    {
        for (j = 0; j < MAX; j++)
            m2[i][j] = m1[j][i];
    }
}
```

**Output:**
```
Enter elements for first array:
Enter the element:1
Enter the element:2
Enter the element:3
Enter the element:2
Enter the element:1
Enter the element:4
Enter the element:4
Enter the element:3
Enter the element:2

Enter elements for second array:
Enter the element:3
Enter the element:2
Enter the element:3
Enter the element:4
Enter the element:3
Enter the element:2
Enter the element:1
Enter the element:3
Enter the element:1

First Array:
1       2       3
2       1       4
4       3       2

Second Array:
3       2       3
4       3       2
1       3       1

After Addition:
4       4       6
6       4       6
5       6       3

After Multiplication:
14      17      10
14      19      12
26      23      20

Transpose of first matrix:
1       2       4
2       1       3
3       4       2
```

In this program we have defined functions `create()` to create an array of ints and function `display()` to display elements of a matrix.

The function `matadd()` adds the elements of two matrices `mat1` and `mat2` and stores the result in the third matrix `mat3`. Similarly, the function `matmul()` multiplies the elements of matrix `mat1` with the elements of matrix `mat2` and stores the result in `mat4`. The function `transpose()`, transposes a matrix. A transpose of a matrix is obtained by interchanging the rows with corresponding columns of a given matrix. The transposed matrix is stored in `mat5`.

---