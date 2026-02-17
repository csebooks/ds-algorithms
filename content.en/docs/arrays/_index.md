---
title: 'Arrays'
weight: 2
references:
    books:
        - b1:
            title: Data Structures and Algorithm Analysis in C by Mark Allen Weiss 
            url: https://mrajacse.files.wordpress.com/2012/08/data-structures-and-algorithm-analysis-in-c-mark-allen-weiss.pdf
        - b2:
            title: Data_Structures_and_Algorithm_Analysis_2e By mark-allen-weiss
            url: https://www.google.co.in/books/edition/Data_Structures_and_Algorithm_Analysis_i/83RWbPynhkgC?hl=en&gbpv=1

---

# Chapter 02: Arrays
## Friends Are Friends

### Why This Chapter Matters?

Array is one data structure that has been used more than any other. Arrays are simple yet reliable and are used in more situations than you can count. Yet they have problems that are typical to them, which at times lead to serious performance issues. They are like old friends. You accept and live with their qualities—good as well as bad.

---

## Data Structures Through C

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

## Arrays

An **Array** is a finite collection of similar elements stored in adjacent memory locations. An array containing n number of elements is referenced using an index that varies from 0 to n-1. For example, the elements of an array `arr[n]` containing n elements are denoted by `arr[0], arr[1], arr[2], ..., arr[n-1]`, where 0 is the lower bound of the array, n-1 is the upper bound of the array and 0, 1, 2, etc. are indices of the array.

**Figure 2-2. Elements in an array with their indices.**

| a[0] | a[1] | a[2] | a[3] | a[4] | a[5] |
|:---:|:---:|:---:|:---:|:---:|:---:|
| 34 | 1 | 5 | -6 | 12 | 9 |

There are several operations that can be performed on an array. These operations are listed in Table 2-1.

**Table 2-1. Operations performed on arrays.**

| Operation | Description |
|-----------|-------------|
| Traversal | Processing each element in the array |
| Search | Finding the location of an element with a given value |
| Insertion | Adding a new element to an array |
| Deletion | Removing an element from an array |
| Sorting | Organizing the array elements in some order |
| Merging | Combining two arrays into a single array |
| Reversing | Reversing the elements of an array |

Let us now see a program that shows how to perform these operations on an array.

---

### Honest Solid Code
**Program 2-1. Implementation of various array operations**

```c
#include <stdio.h>
#define MAX 5

void insert(int *, int pos, int num);
void del(int *, int pos);
void reverse(int *);
void display(int *);
void search(int *, int num);

int main()
{
    int arr[5];
    
    insert(arr, 1, 11);
    insert(arr, 2, 12);
    insert(arr, 3, 13);
    insert(arr, 4, 14);
    insert(arr, 5, 15);
    
    printf("Elements of Array:\n");
    display(arr);
    
    del(arr, 5);
    del(arr, 2);
    printf("After deletion:\n");
    display(arr);
    
    insert(arr, 2, 222);
    insert(arr, 5, 555);
    printf("After insertion:\n");
    display(arr);
    
    reverse(arr);
    printf("After reversing:\n");
    display(arr);
    
    search(arr, 222);
    search(arr, 666);
    
    return 0;
}

/* inserts an element num at given position pos */
void insert(int *arr, int pos, int num)
{
    /* shift elements to right */
    int i;
    for (i = MAX - 1; i >= pos; i--)
        arr[i] = arr[i - 1];
    arr[i] = num;
}

/* deletes an element from the given position pos */
void del(int *arr, int pos)
{
    /* skip to the desired position */
    int i;
    for (i = pos; i < MAX; i++)
        arr[i - 1] = arr[i];
    arr[i - 1] = 0;
}

/* reverses the entire array */
void reverse(int *arr)
{
    int i;
    for (i = 0; i < MAX / 2; i++)
    {
        int temp = arr[i];
        arr[i] = arr[MAX - 1 - i];
        arr[MAX - 1 - i] = temp;
    }
}

/* searches array for a given element num */
void search(int *arr, int num)
{
    int i;
    for (i = 0; i < MAX; i++)
    {
        if (arr[i] == num)
        {
            printf("Element %d is at %dth position\n", num, i + 1);
            return;
        }
    }
    printf("Element %d is absent\n", num);
}

/* displays contents of a array */
void display(int *arr)
{
    int i;
    for (i = 0; i < MAX; i++)
        printf("%d\t", arr[i]);
    printf("\n");
}
```

**Output:**
```
Elements of Array:
11      12      13      14      15
After deletion:
11      13      14      0       0
After insertion:
11      222     13      14      555
After reversing:
555     14      13      222     11
Element 222 is at 4th position
Element 666 is absent
```

In this program we have created an array `arr` which contains 5 ints. We have passed the base address of this array to functions `insert()`, `del()`, `display()`, `reverse()` and `search()` to perform different operations on the array.

The `insert()` function takes two arguments, the position `pos` at which the new number has to be inserted and the number `num` that has to be inserted. In this function, firstly through a loop, we have shifted the numbers from the specified position, one place to the right of their existing position. Then we have placed the number `num` at position `pos`.

The `del()` function deletes the element present at the given position `pos`. For this we have shifted the numbers placed after the position from where the number is to be deleted, one place to the left of their existing positions. The number at position `pos` is then overwritten with 0.

In `reverse()` function we have reversed the entire array by swapping the elements `arr[0]` with `arr[4]`, `arr[1]` with `arr[3]` and so on. Note that swapping should continue for `MAX/2` times only, irrespective of whether MAX is odd or even.

The `search()` function searches the array for the specified number. For this the comparison is carried out until either the list is exhausted or a match is found. If the match is not found then the function displays the relevant message.

In the `display()` function, the entire array is traversed to display the elements of the array.

---

## Two-Dimensional Arrays

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

## Common Matrix Operations

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

## Multidimensional Arrays

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

## Arrays and Polynomials

Polynomials like 5X⁴ + 2X³ + 7X² + 10X - 8 can be maintained using an array. The simplest way to represent a polynomial of degree n is to store the coefficient of (n+1) terms of a polynomial in an array. For this each element of the array should consist of two values—coefficient and exponent. While storing the polynomial it is assumed that the exponent of each successive term is less than that of the previous term. Once we build an array to represent a polynomial, we can use it to perform common polynomial operations like addition and multiplication. The following program demonstrates how we can store polynomials and add them.

### Honest Solid Code
**Program 2-3. Implementation of polynomial addition**

```c
#include <stdio.h>
#define MAX 10

struct term
{
    int coeff;
    int exp;
};

struct poly
{
    struct term t[10];
    int noofterms;
};

void initpoly(struct poly *);
void polyappend(struct poly *, int c, int e);
struct poly polyadd(struct poly, struct poly);
void display(struct poly);

int main()
{
    struct poly p1, p2, p3;
    
    initpoly(&p1);
    initpoly(&p2);
    initpoly(&p3);
    
    polyappend(&p1, 1, 7);
    polyappend(&p1, 2, 6);
    polyappend(&p1, 3, 5);
    polyappend(&p1, 4, 4);
    polyappend(&p1, 5, 2);
    
    polyappend(&p2, 1, 4);
    polyappend(&p2, 1, 3);
    polyappend(&p2, 1, 2);
    polyappend(&p2, 1, 1);
    polyappend(&p2, 2, 0);
    
    p3 = polyadd(p1, p2);
    
    printf("First polynomial:\n");
    display(p1);
    printf("Second polynomial:\n");
    display(p2);
    printf("Resultant polynomial:\n");
    display(p3);
    
    return 0;
}

/* initializes elements of struct poly */
void initpoly(struct poly *p)
{
    int i;
    p->noofterms = 0;
    for (i = 0; i < MAX; i++)
    {
        p->t[i].coeff = 0;
        p->t[i].exp = 0;
    }
}

/* adds the term of polynomial to the array t */
void polyappend(struct poly *p, int c, int e)
{
    p->t[p->noofterms].coeff = c;
    p->t[p->noofterms].exp = e;
    (p->noofterms)++;
}

/* displays the polynomial equation */
void display(struct poly p)
{
    int flag = 0, i;
    for (i = 0; i < p.noofterms; i++)
    {
        if (p.t[i].exp != 0)
            printf("%d x^%d + ", p.t[i].coeff, p.t[i].exp);
        else
        {
            printf("%d", p.t[i].coeff);
            flag = 1;
        }
    }
    if (!flag)
        printf("\b\b ");
    printf("\n");
}

/* adds two polynomials p1 and p2 */
struct poly polyadd(struct poly p1, struct poly p2)
{
    int i, j, c;
    struct poly p3;
    
    initpoly(&p3);
    
    if (p1.noofterms > p2.noofterms)
        c = p1.noofterms;
    else
        c = p2.noofterms;
    
    for (i = 0, j = 0; i <= c; p3.noofterms++)
    {
        if (p1.t[i].coeff == 0 && p2.t[j].coeff == 0)
            break;
        
        if (p1.t[i].exp >= p2.t[j].exp)
        {
            if (p1.t[i].exp == p2.t[j].exp)
            {
                p3.t[p3.noofterms].coeff = p1.t[i].coeff + p2.t[j].coeff;
                p3.t[p3.noofterms].exp = p1.t[i].exp;
                i++;
                j++;
            }
            else
            {
                p3.t[p3.noofterms].coeff = p1.t[i].coeff;
                p3.t[p3.noofterms].exp = p1.t[i].exp;
                i++;
            }
        }
        else
        {
            p3.t[p3.noofterms].coeff = p2.t[j].coeff;
            p3.t[p3.noofterms].exp = p2.t[j].exp;
            j++;
        }
    }
    return p3;
}
```

**Output:**
```
First polynomial:
1 x^7 + 2 x^6 + 3 x^5 + 4 x^4 + 5 x^2 
Second polynomial:
1 x^4 + 1 x^3 + 1 x^2 + 1 x^1 + 2
Resultant polynomial:
1 x^7 + 2 x^6 + 3 x^5 + 5 x^4 + 1 x^3 + 6 x^2 + 1 x^1 + 2
```

In this program the structure `poly` contains another structure element of the type `struct term`. This structure stores the coefficient and exponent of the term of a polynomial. The element `noofterms` stores the total number of terms that a variable of the type `struct poly` is supposed to hold. The function `polyappend()` adds the term of a polynomial to the array `t`. The function `polyadd()` adds the polynomials represented by variables `p1` and `p2`. The function `display()` displays the polynomial.

In `main()`, we have called the function `polyappend()` several times to build two polynomials represented by variables `p1` and `p2`. Next, the function `polyadd()` is called. While doing so we have passed `p1` and `p2` and collected their sum in `p3`. In this function, arrays representing the two polynomials are traversed. While traversing, the polynomials are compared on a term-by-term basis. If the exponents of the two terms being compared are equal then their coefficients are added and the result is stored in the third polynomial. If the exponents of two terms are not equal then the term with the bigger exponent is added to the third polynomial. If the term with an exponent is present in only one of the two polynomials, then that term is added as it is to the third polynomial.

Lastly, the terms of the resulting polynomial are displayed using the function `display()`.

---

## Multiplication of Polynomials

Let us now see a program that carries out multiplication of two polynomials.

### Honest Solid Code
**Program 2-4. Implementation of polynomial multiplication**

```c
#include <stdio.h>
#define MAX 10

struct term
{
    int coeff;
    int exp;
};

struct poly
{
    struct term t[10];
    int noofterms;
};

void initpoly(struct poly *);
void polyappend(struct poly *, int, int);
struct poly polyadd(struct poly, struct poly);
struct poly polymul(struct poly, struct poly);
void display(struct poly);

int main()
{
    struct poly p1, p2, p3;
    
    initpoly(&p1);
    initpoly(&p2);
    initpoly(&p3);
    
    polyappend(&p1, 1, 4);
    polyappend(&p1, 2, 3);
    polyappend(&p1, 2, 2);
    polyappend(&p1, 2, 1);
    
    polyappend(&p2, 2, 3);
    polyappend(&p2, 3, 2);
    polyappend(&p2, 4, 1);
    
    p3 = polymul(p1, p2);
    
    printf("First polynomial:\n");
    display(p1);
    printf("Second polynomial:\n");
    display(p2);
    printf("Resultant polynomial:\n");
    display(p3);
    
    return 0;
}

/* initializes elements of struct poly */
void initpoly(struct poly *p)
{
    int i;
    p->noofterms = 0;
    for (i = 0; i < MAX; i++)
    {
        p->t[i].coeff = 0;
        p->t[i].exp = 0;
    }
}

/* adds the term of polynomial to the array t */
void polyappend(struct poly *p, int c, int e)
{
    p->t[p->noofterms].coeff = c;
    p->t[p->noofterms].exp = e;
    (p->noofterms)++;
}

/* displays the polynomial equation */
void display(struct poly p)
{
    int flag = 0, i;
    for (i = 0; i < p.noofterms; i++)
    {
        if (p.t[i].exp != 0)
            printf("%d x^%d + ", p.t[i].coeff, p.t[i].exp);
        else
        {
            printf("%d", p.t[i].coeff);
            flag = 1;
        }
    }
    if (!flag)
        printf("\b\b ");
    printf("\n");
}

/* adds two polynomials p1 and p2 */
struct poly polyadd(struct poly p1, struct poly p2)
{
    int i, j, c;
    struct poly p3;
    
    initpoly(&p3);
    
    if (p1.noofterms > p2.noofterms)
        c = p1.noofterms;
    else
        c = p2.noofterms;
    
    for (i = 0, j = 0; i <= c; p3.noofterms++)
    {
        if (p1.t[i].coeff == 0 && p2.t[j].coeff == 0)
            break;
        
        if (p1.t[i].exp >= p2.t[j].exp)
        {
            if (p1.t[i].exp == p2.t[j].exp)
            {
                p3.t[p3.noofterms].coeff = p1.t[i].coeff + p2.t[j].coeff;
                p3.t[p3.noofterms].exp = p1.t[i].exp;
                i++;
                j++;
            }
            else
            {
                p3.t[p3.noofterms].coeff = p1.t[i].coeff;
                p3.t[p3.noofterms].exp = p1.t[i].exp;
                i++;
            }
        }
        else
        {
            p3.t[p3.noofterms].coeff = p2.t[j].coeff;
            p3.t[p3.noofterms].exp = p2.t[j].exp;
            j++;
        }
    }
    return p3;
}

/* multiplies two polynomials p1 and p2 */
struct poly polymul(struct poly p1, struct poly p2)
{
    int coeff, exp;
    struct poly temp, p3;
    
    initpoly(&temp);
    initpoly(&p3);
    
    if (p1.noofterms != 0 && p2.noofterms != 0)
    {
        int i;
        for (i = 0; i < p1.noofterms; i++)
        {
            int j;
            struct poly p;
            initpoly(&p);
            
            for (j = 0; j < p2.noofterms; j++)
            {
                coeff = p1.t[i].coeff * p2.t[j].coeff;
                exp = p1.t[i].exp + p2.t[j].exp;
                polyappend(&p, coeff, exp);
            }
            
            if (i != 0)
            {
                p3 = polyadd(temp, p);
                temp = p3;
            }
            else
                temp = p;
        }
    }
    return p3;
}
```

**Output:**
```
First polynomial:
1 x^4 + 2 x^3 + 2 x^2 + 2 x^1 
Second polynomial:
2 x^3 + 3 x^2 + 4 x^1 
Resultant polynomial:
2 x^7 + 7 x^6 + 14 x^5 + 18 x^4 + 14 x^3 + 8 x^2 
```

As in the previous program, here too we have called `polyappend()` function several times to build the two polynomials which are represented by the variables `p1` and `p2`. To carry out multiplication the function `polymul()` is called and `p1` and `p2` are passed to it. It returns the product of polynomials `p1` and `p2` which we have collected in `p3`.

In `polymul()` function, first we have checked that whether the two polynomials `p1` and `p2` are non-empty. If they are not then the control goes in a pair of for loop. Here, each term of first polynomial contained in `p1` is multiplied with every term of second polynomial contained in `p2`. While doing so, we have called `polyappend()` to add the terms to `p`. The first resultant polynomial is stored in temporary variable `temp` of the type `struct poly`. There onwards the function `polyadd()` is called to add the resulting polynomials.

Lastly, the terms of the resulting polynomial are displayed using the function `display()`.

---

## Chapter Bullets
### Summary of chapter

- Array is a collection of similar elements stored in adjacent memory locations.
- Arrays cannot grow or shrink dynamically. Hence, they are useful in situations where number of elements stored in it is fixed.
- Common array operations include traversal, searching, sorting, insertion, deletion, merging and reversal.
- Two-dimensional arrays can be arranged in memory either in row-major or column-major fashion.
- All matrix operations like transpose, addition, multiplication can be implemented using two-dimensional arrays.
- Array of structures can be used to store a polynomial and to perform polynomial operations like addition and multiplication.

---

## Check Your Progress
### Exercise - Level I

**[A] Fill in the blanks:**

(a) A data structure is said to be _____________ if its elements form a sequence.

(b) An Array is a collection of ___________ elements stored in ___________ memory locations.

(c) Index of an array containing n elements varies from _____ to ________.

(d) A 2-D array is also called _______.

**[B] Pick up the correct alternative for each of the following questions:**

(a) To traverse an array means
1. To process each element in an array
2. To delete an element from an array
3. To insert an element into an array
4. To combine two arrays into a single array

(b) A program P reads in 500 integers in the range [0..100] representing the scores of 500 students. It then prints the frequency of each score above 50. What would be the best way for P to store the frequencies?
1. An array of 50 numbers
2. An array of 100 numbers
3. An array of 500 numbers
4. A dynamically allocated array of 550 numbers

(c) Which of the following operations is not O(1) for an array of sorted data. You may assume that array elements are distinct.
1. Find the iᵗʰ largest element
2. Delete an element
3. Find the iᵗʰ smallest element
4. All of the above

---

## Sharpen Your Skills
### Exercise - Level II

**[C] Answer the following:**

(a) Find the location of the element `a[1][2][2][1]` from a 4-D integer array `a[4][3][4][3]` if the base address of the array is 1002.

(b) Design a data structure for a banking system where the maximum number of clients is 150. Information to be stored about clients—name, address, account no., balance, status as Low/Medium/High depending on balance.

(c) Design a data structure for Income Tax department to hold information for maximum 200 persons. Information to be stored about persons—Income Tax no., tax amount, name, address, whether tax paid or not for previous year, group as High/Low depending on amount of tax to be paid and category which would vary from 1 to 5.

**[D] Write programs for the following:**

(a) Write a program to find out the maximum and the second maximum number from an array of integers.

(b) Build an array called chess to represent a chessboard and write a function that would be capable of displaying position of each coin on the chessboard.

(c) There are two arrays A and B. A contains 25 elements, whereas, B contains 30 elements. Write a function to create an array C that contains only those elements that are common to A and B.

---

## Coding Interview Questions
### Exercise Level III

(a) The Mode of an array of numbers is the number m in the array that is repeated most frequently. If more than one number is repeated with equal maximal frequencies, there is no mode. Write a program that accepts an array of numbers and returns the mode or an indication that the mode does not exist.

(b) Write a program to delete duplicate elements from an array of 20 integers.

(c) A square matrix is symmetric if for all values of i and j `a[i][j] = a[j][i]`. Write a program, which verifies whether a given 5×5 matrix is symmetric, or not.

---

## Case Scenario Exercise

### Orthogonal Matrix

A square matrix is said to be **Orthogonal** if the matrix obtained by multiplying the matrix with its transpose is an identity matrix. In other words, if A is a matrix and T is its transpose, then matrix B obtained by multiplying A with T is called orthogonal if it is an identity matrix. An identity matrix is a square matrix in which the elements in the leading diagonal are 1. Write a program that receives a square matrix and determines whether it is Orthogonal or not.

*Orthogonal matrices have applications in field of numerical linear algebra.*

---

### Longest increasing sub-sequence

One of the interesting problems in Computer Science is to find the longest increasing subsequence in a given sequence. The subsequence should be as long as possible and its elements must be in ascending order. The subsequence elements need not be in adjacent locations and the elements need not be distinct.

For example, in the following sequence:
```
0, 8, 4, 12, 2, 10, 6, 14, 1, 9, 5, 13, 3, 11, 7, 15
```

the longest increasing subsequence is:
```
0, 2, 6, 9, 11, 15
```

This subsequence has length six; the input sequence has no seven-member increasing subsequences. The longest increasing subsequence in this example is not unique. `0, 4, 6, 9, 11, 15` or `0, 4, 6, 9, 13, 15` are other increasing subsequences of equal length in the same input sequence.

Write a program to obtain the longest increasing subsequence in a given sequence.

*Longest increasing subsequences have applications in fields of random matrix theory, representation theory, and physics.*

---
