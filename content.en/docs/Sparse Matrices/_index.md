---
title: 'Sparse Matrices'
weight: 4
references:
    books:
        - b1:
            title: Data Structures and Algorithm Analysis in C by Mark Allen Weiss 
            url: https://mrajacse.files.wordpress.com/2012/08/data-structures-and-algorithm-analysis-in-c-mark-allen-weiss.pdf
        - b2:
            title: Data_Structures_and_Algorithm_Analysis_2e By mark-allen-weiss
            url: https://www.google.co.in/books/edition/Data_Structures_and_Algorithm_Analysis_i/83RWbPynhkgC?hl=en&gbpv=1

---


# Chapter 4: Sparse Matrices
## Lean Is Better

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

## Representation of Sparse Matrix as an Array

Let us see a program that accepts elements of a sparse matrix and creates an array containing 3-tuples of non-zero elements present in the sparse matrix.

### Program 4-1: Sparse Matrix in 3-tuple form

```c
#include <stdio.h>
#include <stdlib.h>

#define MAX1 3
#define MAX2 3

struct sparse {
    int *sp;
    int row;
};

void initsparse(struct sparse *);
void create_array(struct sparse *);
void display(struct sparse);
int count(struct sparse);
void create_tuple(struct sparse *, struct sparse);
void display_tuple(struct sparse);
void delsparse(struct sparse *);

int main() {
    struct sparse s1, s2;
    int c;
    
    initsparse(&s1);
    initsparse(&s2);
    
    create_array(&s1);
    printf("Elements in Sparse Matrix:");
    display(s1);
    
    c = count(s1);
    printf("Number of non-zero elements: %d\n\n", c);
    
    create_tuple(&s2, s1);
    printf("Array of non-zero elements:");
    display_tuple(s2);
    
    delsparse(&s1);
    delsparse(&s2);
    
    return 0;
}

/* initialises element of structure */
void initsparse(struct sparse *p) {
    p->sp = NULL;
}

/* dynamically creates the matrix of size MAX1 x MAX2 */
void create_array(struct sparse *p) {
    int n, i;
    p->sp = (int *)malloc(MAX1 * MAX2 * sizeof(int));
    
    for (i = 0; i < MAX1 * MAX2; i++) {
        printf("Enter element no. %d: ", i);
        scanf("%d", &n);
        *(p->sp + i) = n;
    }
    printf("\n");
}

/* displays the contents of the matrix */
void display(struct sparse p) {
    int i;
    /* traverses the entire matrix */
    for (i = 0; i < MAX1 * MAX2; i++) {
        /* positions the cursor to the new line for every new row */
        if (i % MAX2 == 0)
            printf("\n");
        printf("%d\t", *(p.sp + i));
    }
    printf("\n\n");
}

/* counts the number of non-zero elements */
int count(struct sparse p) {
    int cnt = 0, i;
    for (i = 0; i < MAX1 * MAX2; i++) {
        if (*(p.sp + i) != 0)
            cnt++;
    }
    return cnt;
}

/* creates an array that stores information about non-zero elements */
void create_tuple(struct sparse *p, struct sparse s) {
    int r = 0, c = -1, l = -1, i;
    
    p->row = count(s) + 1;
    p->sp = (int *)malloc(p->row * 3 * sizeof(int));
    
    *(p->sp + 0) = MAX1;
    *(p->sp + 1) = MAX2;
    *(p->sp + 2) = p->row - 1;
    l = 2;
    
    for (i = 0; i < MAX1 * MAX2; i++) {
        c++;
        /* sets the row and column values */
        if (((i % MAX2) == 0) && (i != 0)) {
            r++;
            c = 0;
        }
        /* checks for non-zero element, row, column and non-zero element value is assigned to the matrix */
        if (*(s.sp + i) != 0) {
            l++;
            *(p->sp + l) = r;
            l++;
            *(p->sp + l) = c;
            l++;
            *(p->sp + l) = *(s.sp + i);
        }
    }
}

/* displays the contents of 3-tuple */
void display_tuple(struct sparse p) {
    int i;
    for (i = 0; i < p.row * 3; i++) {
        if (i % 3 == 0)
            printf("\n");
        printf("%d\t", *(p.sp + i));
    }
}

/* deallocates memory */
void delsparse(struct sparse *p) {
    free(p->sp);
}
```

### Output:
```
Enter element no. 0: 0
Enter element no. 1: 2
Enter element no. 2: 0
Enter element no. 3: 9
Enter element no. 4: 0
Enter element no. 5: 1
Enter element no. 6: 0
Enter element no. 7: 0
Enter element no. 8: -4

Elements in Sparse Matrix:
0	2	0	
9	0	1	
0	0	-4	

Number of non-zero elements: 4

Array of non-zero elements:
3	3	4	
0	1	2	
1	0	9	
2	2	-4	
```

In this program we have designed a structure called `sparse`. In the `create_array()` function, we have dynamically created a matrix of size `MAX1 x MAX2`. The values for the matrix are accepted through keyboard. The `display()` function displays the contents of the sparse matrix and the `count()` function counts the total number of non-zero elements present in sparse matrix.

The `create_tuple()` function creates a 2-D array dynamically. But the question arises as how much memory should get allocated for this array? Since each row in the 3-tuple form represents a non-zero element in the original array the new array should contain as many rows as the number of non-zero elements in the original matrix. From the 3-tuple form we must be able to build the original array. Hence the very first row in the new array should contain number of rows, number of columns and number of non-zero elements in the original array.

In the program we have determined the size of the new array through the following statements:

```c
p->row = count(s) + 1;
p->sp = (int *)malloc(p->row * 3 * sizeof(int));
```

In the first statement we have obtained the count of non-zero elements present in the given array. To that count we have added 1. The first row (i.e., 0th row) in this array stores the information about the total number of rows, columns and non-zero elements present in the given array. From second row (i.e., 1st row) onwards this array stores the row and column position of a non-zero element and the value of the non-zero element.

Since the number of rows in the array depends on the number of non-zero elements in the given array, we have created the array dynamically. The number of columns in this array would always be 3. The 0th column stores the row number of the non-zero element. The 1st column stores the column number of the non-zero element and the 2nd column stores the value of non-zero element.

Lastly, the `display_tuple()` function displays the contents of 3-tuple.

---

## Common Matrix Operations

Common matrix operations are addition, multiplication, transposition, etc. Let us see how these operations are carried out on a sparse matrix implemented as an array. Note that each program that we are going to discuss now consists of functions—`create_array()`, `create_tuple()`, `display()`, `display_tuple()` and `count()`. We have already seen the working of these functions in previous program. Hence, we shall discuss only the function(s) that perform given matrix operation.

---

## Transpose of a Sparse Matrix

Following program accepts elements of a sparse matrix, creates a 3-tuple form of non-zero elements present in the sparse matrix and then obtains a transpose of the sparse matrix from the 3-tuple form.

### Program 4-2: Transpose of a Sparse Matrix

```c
#include <stdio.h>
#include <stdlib.h>

#define MAX1 3
#define MAX2 3

struct sparse {
    int *sp;
    int row;
};

void initsparse(struct sparse *);
void create_array(struct sparse *);
void display(struct sparse);
int count(struct sparse);
void create_tuple(struct sparse *, struct sparse);
void display_tuple(struct sparse);
void transpose(struct sparse *, struct sparse);
void display_transpose(struct sparse);
void delsparse(struct sparse *);

int main() {
    struct sparse s[3];
    int c, i;
    
    for (i = 0; i <= 2; i++)
        initsparse(&s[i]);
    
    create_array(&s[0]);
    printf("Elements in Sparse Matrix:");
    display(s[0]);
    
    c = count(s[0]);
    printf("Number of non-zero elements: %d\n\n", c);
    
    create_tuple(&s[1], s[0]);
    printf("Array of non-zero elements:");
    display_tuple(s[1]);
    
    transpose(&s[2], s[1]);
    printf("Transpose of array:");
    display_transpose(s[2]);
    
    for (i = 0; i <= 2; i++)
        delsparse(&s[i]);
    
    return 0;
}

/* initialises structure elements */
void initsparse(struct sparse *p) {
    p->sp = NULL;
}

/* dynamically creates the matrix of size MAX1 x MAX2 */
void create_array(struct sparse *p) {
    int n, i;
    p->sp = (int *)malloc(MAX1 * MAX2 * sizeof(int));
    
    for (i = 0; i < MAX1 * MAX2; i++) {
        printf("Enter element no. %d: ", i);
        scanf("%d", &n);
        *(p->sp + i) = n;
    }
    printf("\n");
}

/* displays the contents of the matrix */
void display(struct sparse s) {
    int i;
    /* traverses the entire matrix */
    for (i = 0; i < MAX1 * MAX2; i++) {
        /* positions the cursor to the new line for every new row */
        if (i % MAX2 == 0)
            printf("\n");
        printf("%d\t", *(s.sp + i));
    }
    printf("\n\n");
}

/* counts the number of non-zero elements */
int count(struct sparse s) {
    int cnt = 0, i;
    for (i = 0; i < MAX1 * MAX2; i++) {
        if (*(s.sp + i) != 0)
            cnt++;
    }
    return cnt;
}

/* creates an array that stores information about non-zero elements */
void create_tuple(struct sparse *p, struct sparse s) {
    int r = 0, c = -1, l = -1, i;
    
    p->row = count(s) + 1;
    p->sp = (int *)malloc(p->row * 3 * sizeof(int));
    
    *(p->sp + 0) = MAX1;
    *(p->sp + 1) = MAX2;
    *(p->sp + 2) = p->row - 1;
    l = 2;
    
    for (i = 0; i < MAX1 * MAX2; i++) {
        c++;
        /* sets the row and column values */
        if (((i % MAX2) == 0) && (i != 0)) {
            r++;
            c = 0;
        }
        /* checks for non-zero element, row, column and non-zero element value is assigned to the matrix */
        if (*(s.sp + i) != 0) {
            l++;
            *(p->sp + l) = r;
            l++;
            *(p->sp + l) = c;
            l++;
            *(p->sp + l) = *(s.sp + i);
        }
    }
}

/* displays the contents of 3-tuple */
void display_tuple(struct sparse p) {
    int i;
    for (i = 0; i < p.row * 3; i++) {
        if (i % 3 == 0)
            printf("\n");
        printf("%d\t", *(p.sp + i));
    }
    printf("\n\n");
}

/* obtains transpose of an array */
void transpose(struct sparse *p, struct sparse s) {
    int x, q, pos_1, pos_2, col, elem, c, y;
    
    /* allocate memory */
    p->sp = (int *)malloc(s.row * 3 * sizeof(int));
    p->row = s.row;
    
    /* store total number of rows, cols and non-zero elements */
    *(p->sp + 0) = *(s.sp + 1);
    *(p->sp + 1) = *(s.sp + 0);
    *(p->sp + 2) = *(s.sp + 2);
    
    col = *(p->sp + 1);
    elem = *(p->sp + 2);
    
    if (elem <= 0)
        return;
    
    x = 1;
    for (c = 0; c < col; c++) {
        for (y = 1; y <= elem; y++) {
            q = y * 3 + 1;
            if (*(s.sp + q) == c) {
                pos_2 = x * 3 + 0;
                pos_1 = y * 3 + 1;
                *(p->sp + pos_2) = *(s.sp + pos_1);
                
                pos_2 = x * 3 + 1;
                pos_1 = y * 3 + 0;
                *(p->sp + pos_2) = *(s.sp + pos_1);
                
                pos_2 = x * 3 + 2;
                pos_1 = y * 3 + 2;
                *(p->sp + pos_2) = *(s.sp + pos_1);
                
                x++;
            }
        }
    }
}

/* displays 3-tuple after transpose operation */
void display_transpose(struct sparse p) {
    int i;
    for (i = 0; i < p.row * 3; i++) {
        if (i % 3 == 0)
            printf("\n");
        printf("%d\t", *(p.sp + i));
    }
}

/* deallocates memory */
void delsparse(struct sparse *p) {
    free(p->sp);
}
```

### Output:
```
Enter element no. 0: 4
Enter element no. 1: 0
Enter element no. 2: 0
Enter element no. 3: 1
Enter element no. 4: 0
Enter element no. 5: 3
Enter element no. 6: -2
Enter element no. 7: 0
Enter element no. 8: 0

Elements in Sparse Matrix:
4	0	0	
1	0	3	
-2	0	0	

Number of non-zero elements: 4

Array of non-zero elements:
3	3	4	
0	0	4	
0	2	1	
1	2	3	
2	0	-2	

Transpose of array:
3	3	4	
0	0	4	
2	0	1	
2	1	3	
0	2	-2	
```

In the `transpose()` function first we have allocated memory required to store the elements in the target 3-tuple. Next, we have stored the total number of rows, columns and non-zero elements that this 3-tuple will hold. This is achieved through the following three statements:

```c
*(p->sp + 0) = *(s.sp + 1);
*(p->sp + 1) = *(s.sp + 0);
*(p->sp + 2) = *(s.sp + 2);
```

Note that, here in `p->sp`, the place where total number of rows should get stored we have stored total number of columns. Similarly in place where total number of columns should get stored, we have stored total number of rows. This is because in case of transpose operation total number rows become equal to total number of columns and vice versa.

The transpose operation is carried out through a pair of for loops. The outer for loop runs till the non-zero elements of col number of columns (of source 3-tuple) are not scanned. In the inner for loop first we have obtained the position at which the column number of a non-zero element is stored (in the source 3-tuple) through the statement:

```c
q = y * 3 + 1;
```

Then we have checked whether the column number of a non-zero element matches with the column number currently being considered i.e., c. If the two values match, then the information is stored in the target 3-tuple through the statements given below:

```c
pos_2 = x * 3 + 0;
pos_1 = y * 3 + 1;
*(p->sp + pos_2) = *(s.sp + pos_1);
```

The variable `pos_2` is used for the target 3-tuple, to store the position at which data from source 3-tuple should get copied. Similarly, the variable `pos_1` is used for the source 3-tuple, to extract data from it. The third statement copies the column position of a non-zero element from source 3-tuple to the target 3-tuple. This column number gets stored at the row position in target 3-tuple.

On similar lines the row position of a non-zero element of source 3-tuple is copied at the column position of the target 3-tuple through the following statements:

```c
pos_2 = x * 3 + 1;
pos_1 = y * 3 + 0;
*(p->sp + pos_2) = *(s.sp + pos_1);
```

Finally, the non-zero value from source 3-tuple is copied to the target 3-tuple through the following statements:

```c
pos_2 = x * 3 + 2;
pos_1 = y * 3 + 2;
*(p->sp + pos_2) = *(s.sp + pos_1);
```

The target 3-tuple thus obtained is nothing but a transpose of an array that user has entered through `create_array()` function. But the target 3-tuple stores the information of non-zero elements. The elements in this 3-tuple are then displayed by calling `display_transpose()` function.

---

## Addition of Sparse Matrices

Let us now see a program that carries out addition of two sparse matrices represented in 3-tuple form. Here is the program...

### Program 4-3: Addition of Sparse Matrices

```c
#include <stdio.h>
#include <stdlib.h>

#define MAX1 3
#define MAX2 3
#define MAXSIZE 9
#define BIGNUM 100

struct sparse {
    int *sp;
    int row;
    int *result;
};

void initsparse(struct sparse *);
void create_array(struct sparse *);
int count(struct sparse);
void display(struct sparse);
void create_tuple(struct sparse *, struct sparse);
void display_tuple(struct sparse);
void addmat(struct sparse *, struct sparse, struct sparse);
void display_result(struct sparse);
void delsparse(struct sparse *);

int main() {
    struct sparse s[5];
    int i;
    
    for (i = 0; i <= 4; i++)
        initsparse(&s[i]);
    
    create_array(&s[0]);
    create_tuple(&s[1], s[0]);
    display_tuple(s[1]);
    
    create_array(&s[2]);
    create_tuple(&s[3], s[2]);
    display_tuple(s[3]);
    
    addmat(&s[4], s[1], s[3]);
    printf("Result of addition of two matrices:");
    display_result(s[4]);
    
    for (i = 0; i <= 4; i++)
        delsparse(&s[i]);
    
    return 0;
}

/* initialises structure elements */
void initsparse(struct sparse *p) {
    p->sp = NULL;
    p->result = NULL;
}

/* dynamically creates the matrix */
void create_array(struct sparse *p) {
    int n, i;
    
    /* allocate memory */
    p->sp = (int *)malloc(MAX1 * MAX2 * sizeof(int));
    
    /* add elements to the array */
    for (i = 0; i < MAX1 * MAX2; i++) {
        printf("Enter element no. %d: ", i);
        scanf("%d", &n);
        *(p->sp + i) = n;
    }
    printf("\n");
}

/* displays the contents of the matrix */
void display(struct sparse s) {
    int i;
    /* traverses the entire matrix */
    for (i = 0; i < MAX1 * MAX2; i++) {
        /* positions the cursor to the new line for every new row */
        if (i % MAX2 == 0)
            printf("\n");
        printf("%d\t", *(s.sp + i));
    }
    printf("\n\n");
}

/* counts the number of non-zero elements */
int count(struct sparse s) {
    int cnt = 0, i;
    for (i = 0; i < MAX1 * MAX2; i++) {
        if (*(s.sp + i) != 0)
            cnt++;
    }
    return cnt;
}

/* creates an array that stores information about non-zero elements */
void create_tuple(struct sparse *p, struct sparse s) {
    int r = 0, c = -1, l = -1, i;
    
    /* get the total number of non-zero elements
       and add 1 to store total no. of rows, cols, and non-zero values */
    p->row = count(s) + 1;
    
    /* allocate memory */
    p->sp = (int *)malloc(p->row * 3 * sizeof(int));
    
    /* store information about total no. of rows, cols, and non-zero values */
    *(p->sp + 0) = MAX1;
    *(p->sp + 1) = MAX2;
    *(p->sp + 2) = p->row - 1;
    l = 2;
    
    /* scan the array and store info. about non-zero values in the 3-tuple */
    for (i = 0; i < MAX1 * MAX2; i++) {
        c++;
        /* sets the row and column values */
        if (((i % MAX2) == 0) && (i != 0)) {
            r++;
            c = 0;
        }
        /* checks for non-zero element, row, column and non-zero element value is assigned to the matrix */
        if (*(s.sp + i) != 0) {
            l++;
            *(p->sp + l) = r;
            l++;
            *(p->sp + l) = c;
            l++;
            *(p->sp + l) = *(s.sp + i);
        }
    }
}

/* displays the contents of the matrix */
void display_tuple(struct sparse s) {
    int i, j;
    /* traverses the entire matrix */
    printf("Elements in a 3-tuple:\n");
    j = (*(s.sp + 2) + 1) * 3;
    for (i = 0; i < j; i++) {
        /* positions the cursor to the new line for every new row */
        if (i % 3 == 0)
            printf("\n");
        printf("%d\t", *(s.sp + i));
    }
    printf("\n\n");
}

/* carries out addition of two matrices */
void addmat(struct sparse *p, struct sparse s1, struct sparse s2) {
    int i = 1, j = 1, k = 1;
    int elem = 1;
    int max, amax, bmax;
    int rowa, rowb, cola, colb, vala, valb;
    
    /* get the total number of non-zero values from both matrices */
    amax = *(s1.sp + 2);
    bmax = *(s2.sp + 2);
    max = amax + bmax;
    
    /* allocate memory for result */
    p->result = (int *)malloc(MAXSIZE * 3 * sizeof(int));
    
    while (elem <= max) {
        /* check if i < max. non-zero values in first 3-tuple and get the values */
        if (i <= amax) {
            rowa = *(s1.sp + i * 3 + 0);
            cola = *(s1.sp + i * 3 + 1);
            vala = *(s1.sp + i * 3 + 2);
        }
        else
            rowa = cola = BIGNUM;
        
        /* check if j < max. non-zero values in second 3-tuple and get the values */
        if (j <= bmax) {
            rowb = *(s2.sp + j * 3 + 0);
            colb = *(s2.sp + j * 3 + 1);
            valb = *(s2.sp + j * 3 + 2);
        }
        else
            rowb = colb = BIGNUM;
        
        /* if row no. of both 3-tuple are same */
        if (rowa == rowb) {
            /* if col no. of both 3-tuple are same */
            if (cola == colb) {
                /* add two non-zero values, store in result */
                *(p->result + k * 3 + 0) = rowa;
                *(p->result + k * 3 + 1) = cola;
                *(p->result + k * 3 + 2) = vala + valb;
                i++;
                j++;
                max--;
            }
            /* if col no. of first 3-tuple is < col no. of second 3-tuple, then add info. as it is to result */
            if (cola < colb) {
                *(p->result + k * 3 + 0) = rowa;
                *(p->result + k * 3 + 1) = cola;
                *(p->result + k * 3 + 2) = vala;
                i++;
            }
            /* if col no. of first 3-tuple is > col no. of second 3-tuple, then add info. as it is to result */
            if (cola > colb) {
                *(p->result + k * 3 + 0) = rowb;
                *(p->result + k * 3 + 1) = colb;
                *(p->result + k * 3 + 2) = valb;
                j++;
            }
            k++;
        }
        /* if row no. of first 3-tuple is < row no. of second 3-tuple, then add info. as it is to result */
        if (rowa < rowb) {
            *(p->result + k * 3 + 0) = rowa;
            *(p->result + k * 3 + 1) = cola;
            *(p->result + k * 3 + 2) = vala;
            i++;
            k++;
        }
        /* if row no. of first 3-tuple is > row no. of second 3-tuple, then add info. as it is to result */
        if (rowa > rowb) {
            *(p->result + k * 3 + 0) = rowb;
            *(p->result + k * 3 + 1) = colb;
            *(p->result + k * 3 + 2) = valb;
            j++;
            k++;
        }
        elem++;
    }
    
    /* add info about the total no. of rows, cols, and non-zero values that the resultant array contains to the result */
    *(p->result + 0) = MAX1;
    *(p->result + 1) = MAX2;
    *(p->result + 2) = max;
}

/* displays the contents of the matrix */
void display_result(struct sparse s) {
    int i;
    /* traverses the entire matrix */
    for (i = 0; i < (*(s.result + 2) + 1) * 3; i++) {
        /* positions the cursor to the new line for every new row */
        if (i % 3 == 0)
            printf("\n");
        printf("%d\t", *(s.result + i));
    }
    printf("\n\n");
}

/* deallocates memory */
void delsparse(struct sparse *p) {
    if (p->sp != NULL)
        free(p->sp);
    if (p->result != NULL)
        free(p->result);
}
```

### Output:
```
Enter element no. 0: 1
Enter element no. 1: 0
Enter element no. 2: 2
Enter element no. 3: 0
Enter element no. 4: 3
Enter element no. 5: 0
Enter element no. 6: 4
Enter element no. 7: 0
Enter element no. 8: 0

Elements in a 3-tuple:
3	3	4	
0	0	1	
0	2	2	
1	1	3	
2	0	4	

Enter element no. 0: 0
Enter element no. 1: 0
Enter element no. 2: 0
Enter element no. 3: 1
Enter element no. 4: 0
Enter element no. 5: 2
Enter element no. 6: 0
Enter element no. 7: 9
Enter element no. 8: 0

Elements in a 3-tuple:
3	3	3	
1	0	1	
1	2	2	
2	1	9	

Result of addition of two matrices:
3	3	7	
0	0	1	
0	2	2	
1	0	1	
1	1	3	
1	2	2	
2	0	4	
2	1	9	
```

The function `addmat()` carries out addition of two sparse matrices. In this function firstly we have obtained the total number of non-zero elements that the target 3-tuple would hold. This has been achieved through the following statements:

```c
amax = *(s1.sp + 2);
bmax = *(s2.sp + 2);
max = amax + bmax;
```

Then we have allocated memory for the target 3-tuple that would store the result obtained from addition. Through a while loop we have carried out the addition operation. The variables `i` and `j` are used as counters for first 3-tuple (pointed to by `s1.sp`) and second 3-tuple (pointed to by `s2.sp`) respectively. Then we have retrieved the row number, column number and the non-zero value of ith and jth non-zero element respectively. The following cases are considered while performing addition.

(a) If the row numbers as well as column numbers of the non-zero values retrieved from first and second 3-tuple (pointed to by `s1.sp` and `s2.sp` respectively) are same then we have added two non-zero values `vala` and `valb`. The row number `rowa`, column number `cola` and `vala + valb` is then copied to the target 3-tuple pointed to by `result`.

(b) If column number of first 3-tuple is less than the column number of second 3-tuple, then we have added the information about the ith non-zero value of first 3-tuple to the target 3-tuple.

(c) If column number of first 3-tuple is greater than the column number of second 3-tuple, then we have added the information about the jth non-zero value of second 3-tuple to the target 3-tuple.

(d) If row number of first 3-tuple is less than the row number of second 3-tuple, then we have added the information about the ith non-zero value of first 3-tuple to the target 3-tuple.

(e) If row number of first 3-tuple is greater than the row number of second 3-tuple, then we have added the information about the jth non-zero value of second 3-tuple to the target 3-tuple.

Finally, the total number of rows, columns and non-zero values that the target 3-tuple holds is stored in the zeroth row of the target 3-tuple (pointed to by `result`). The function `display_result()` displays result of the addition operation.

---

## Linked Representation of a Sparse Matrix

Representing a sparse matrix as an array of 3-tuples suffers from one important limitation. When we carry out addition or multiplication it is not possible to predict beforehand how many elements in the resultant matrix would be non-zero. As a result, it is not possible to predict the size of the resultant matrix beforehand. Instead of an array we can represent the sparse matrix in the form of a linked list.

In the linked list representation, a separate list is maintained for each column as well as each row of the matrix, i.e., if the matrix is of size 3 x 3, then there would be 3 lists for 3 columns and 3 lists for 3 rows. A node in a list stores the information about the non-zero element of the sparse matrix. The head node for a column list stores the column number, a pointer to the node, which comes first in the column, and a pointer to the next column head node. Thus, the structure for column head node would be as shown below:

```c
struct cheadnode {
    struct node *down;
    int colno;
    struct cheadnode *next;
};
```

A head node for a row list stores, a pointer to the node, which comes first in the row list, and a pointer to the next row head node. The structure for row head node would be as shown below:

```c
struct rheadnode {
    struct rheadnode *next;
    int rowno;
    struct node *right;
};
```

A node on the other hand stores the row number, column number and the value of the non-zero element of the sparse matrix. It also stores a pointer to the node that is immediately to the right of the node in the row list as well as a pointer to the node that is immediately below the node in the column list. The structure for a node would be as shown below:

```c
struct node {
    int row;
    int col;
    int val;
    struct node *down;
    struct node *right;
};
```

In addition to this a special node is used to store the total number of rows, total number of columns, a pointer to the first row head node and a pointer to the first column head node. The information stored in this special node is used for traversing the list. The structure of this special node would be as shown below:

```c
struct spmat {
    struct rheadnode *firstrow;
    int noofrows;
    int noofcols;
    struct cheadnode *firstcol;
};
```

If a particular column list is empty then the field `down` of the column head node would be NULL. Similarly, if a row list is empty then the field `right` of the row head node would be empty. If a node is the last node in a particular column list or a particular row list then the field `down` or the field `right` of the node would be NULL.

Figure 4-2 gives pictorial representation of linked list of a sparse matrix of size 3×3.

**Figure 4-2: Linked Representation of a sparse matrix**

```
Special Head Node
┌─────────┬─────┬─────┐
│ firstrow│  3  │first│  noofrows=3, noofcols=3
│   ↓     │     │col  │
└────┬────┴─────┴──┬──┘
     │             │
     ▼             ▼
rhead[0]      chead[0]
┌─────┬───┬───┐   ┌───┬───┬───┐
│next │ 0 │right│   │down│ 0 │next│
│  ↓  │   │  ↓  │   │ ↓  │   │ ↓  │
└──┬──┴───┴──┬──┘   └──┬─┴───┴──┬─┘
   │         │         │        │
   ▼         ▼         ▼        ▼
rhead[1]   [0,0,2]   [0,0,2]  chead[1]
┌─────┬───┬───┐   ┌───┬───┐   ┌───┬───┬───┐
│next │ 1 │right│   │ N │ N │   │ N │ 1 │next│
│  ↓  │   │  ↓  │   └───┴───┘   │   │   │ ↓  │
└──┬──┴───┴──┬──┘               └───┴───┴──┬─┘
   │         │                              │
   ▼         ▼                              ▼
rhead[2]   [1,0,11]                      chead[2]
┌─────┬───┬───┐                           ┌───┬───┬───┐
│  N  │ 2 │right│                          │   │ 2 │ N │
└─────┴───┴───┘                           └───┴───┴───┘
                │
                ▼
           [0,2,7]
           ┌───┬───┐
           │ N │ N │
           └───┴───┘
```

---

## Other Forms of a Sparse Matrix

A square sparse matrix can be of following types:

| Type | Description |
|:---|:---|
| **Diagonal** | Where the non-zero elements are stored on the leading diagonal of the matrix. |
| **Tridiagonal** | Where the non-zero elements are placed below or above the leading diagonal. |
| **Lower Triangular** | Where the non-zero elements are placed below the leading diagonal. |
| **Upper Triangular** | Where the non-zero elements are placed above the leading diagonal. |

Figure 4-3 illustrates these four matrices.

**Figure 4-3: Different forms of Sparse matrices**

```
Diagonal Matrix          Tridiagonal Matrix
┌───┬───┬───┬───┐       ┌───┬───┬───┬───┐
│ 4 │ 0 │ 0 │ 0 │       │ 0 │ 3 │ 0 │ 0 │
├───┼───┼───┼───┤       ├───┼───┼───┼───┤
│ 0 │ 1 │ 0 │ 0 │       │ 0 │ 0 │ 8 │ 0 │
├───┼───┼───┼───┤       ├───┼───┼───┼───┤
│ 0 │ 0 │ 9 │ 0 │       │ 0 │ 0 │ 0 │ 5 │
├───┼───┼───┼───┤       ├───┼───┼───┼───┤
│ 0 │ 0 │ 0 │12 │       │ 0 │ 0 │ 0 │ 0 │
└───┴───┴───┴───┘       └───┴───┴───┴───┘

Lower Triangular Matrix  Upper Triangular Matrix
┌───┬───┬───┬───┐       ┌───┬───┬───┬───┐
│ 0 │ 0 │ 0 │ 0 │       │ 0 │ 4 │ 0 │ 3 │
├───┼───┼───┼───┤       ├───┼───┼───┼───┤
│13 │ 0 │ 0 │ 0 │       │ 0 │ 0 │ 1 │ 0 │
├───┼───┼───┼───┤       ├───┼───┼───┼───┤
│ 9 │ 2 │ 0 │ 0 │       │ 0 │ 0 │ 0 │ 9 │
├───┼───┼───┼───┤       ├───┼───┼───┼───┤
│ 6 │ 0 │12 │ 0 │       │ 0 │ 0 │ 0 │ 0 │
└───┴───┴───┴───┘       └───┴───┴───┴───┘
```

---

## Chapter Bullets: Summary of Chapter

(a) If many elements from a matrix have a value 0 then the matrix is known as a sparse matrix.

(b) A common way of representing non-zero elements of a sparse matrix is the 3-tuple form.

(c) Sparse matrix can be represented using either an array or a linked list.

(d) A square sparse matrix may take the form of a Diagonal, Tridiagonal, Lower Triangular or Upper Triangular matrix.

---

## Check Your Progress

### Exercise - Level I

**[A] Pick up the correct alternative for each of the following questions:**

(f) A matrix is called sparse when
1. Most of its elements are non-zero
2. Most of its elements are zero
3. All of its elements are non-zero
4. None of the above

(g) In the linked representation of a sparse matrix the head node for a column list stores
1. A pointer to the next column head node
2. A pointer to the first node in column list
3. Column number
4. All of the above

(h) A sparse matrix can be lower-triangular matrix
1. When all the non-zero elements lie only on the leading diagonal.
2. When all the non-zero elements lie above leading diagonal.
3. When all the non-zero elements lie below leading diagonal.
4. Both (3) and (4)

---

### Exercise - Level II

**[B] Answer the following:**

(a) Write a program to build a sparse matrix as an array. Write functions to check if the sparse matrix is a square, diagonal, lower triangular, upper triangular or tridiagonal matrix.

(b) Write a program to subtract two sparse matrices implemented as an array.

(c) Write a program to build a sparse matrix as a linked list. The program should provide functions for following operations:
   - (i) Store an element when the row number, column number and the value is provided
   - (ii) Retrieve an element for given row and column of matrix
   - (iii) Add two sparse matrices
   - (iv) Subtract two sparse matrices

---

### Exercise Level III: Coding Interview Questions

Write a program that carries out multiplication of two sparse matrices through their 3-tuple form and stores the result in another sparse matrix in 3-tuple form.

---

### Case Scenario Exercise: Linked representation of Sparse Matrix

Write a program that stores sparse matrix in the linked list form. The skeleton code for this program is given below. You are required to define different functions whose prototypes are given in the skeleton code and then call these functions from main().

```c
#define MAX1 3
#define MAX2 3

/* structure for col head node */
struct cheadnode {
    int colno;
    struct node *down;
    struct cheadnode *next;
};

/* structure for row head node */
struct rheadnode {
    int rowno;
    struct node *right;
    struct rheadnode *next;
};

/* structure for node to store element */
struct node {
    int row, col, val;
    struct node *right;
    struct node *down;
};

/* structure for special head node */
struct spmat {
    struct rheadnode *firstrow;
    struct cheadnode *firstcol;
    int noofrows;
    int noofcols;
};

struct sparse {
    int *sp;
    int row;
    struct spmat *smat;
    struct cheadnode *chead[MAX2];
    struct rheadnode *rhead[MAX1];
    struct node *nd;
};

void initsparse(struct sparse *);
void create_array(struct sparse *);
void display(struct sparse);
int count(struct sparse);
void create_triplet(struct sparse *, struct sparse);
void create_llist(struct sparse *);
void insert(struct sparse *, struct spmat *, int, int, int);
void show_llist(struct sparse);
void delsparse(struct sparse *);
```
```

## Summary of Corrections Made:

1. **Page 91**: Fixed incomplete sentence "how to conserve this memory and still work with matrices as" to "how to conserve this memory and still work with matrices efficiently"

2. **Page 92**: Fixed "7_{n}percent" to "71 percent", "ercent" to "percent", "meagerly" spelling, fixed "Z x\" to "7 x 7", fixed array initialization syntax

3. **Page 93**: Fixed `#define MAX13` to `#define MAX1 3` and `#define MAX23` to `#define MAX2 3`, fixed `{c` artifact

4. **Page 94**: Fixed `p\rightarrow s p=\mathsf{N U L L}` to `p->sp = NULL`, fixed `p\rightarrow s p=(i n t^{*})malloc` to proper C syntax

5. **Page 95**: Fixed `printf ((n{}^{n})` to `printf("\n")`

6. **Page 96**: Fixed garbled `create_tuple` function with `in\mathsf{r}=0\;,\mathsf{c}=-1,\ ,-1,\textsf{i}\;;` etc. to proper C code, fixed `(p-rightarrow p+0)=` artifact

7. **Page 97**: Fixed output formatting

8. **Page 98**: Fixed `\mathsf\mathsf p\\to\\mathsf o\\mathsf r\ r r o\mathsfmathsf=\mathsf c{c o u n t}` to `p->row = count(s) + 1`

9. **Page 99**: Fixed `void transpose (struct sparse \ {}^{*},struct sparse )` to `void transpose(struct sparse *, struct sparse)`

10. **Page 100**: Fixed `p\rightarrow s\mathsf{P}=\mathsf{N U L L}` to `p->sp = NULL`

11. **Page 101**: Fixed `printf (pi n^{n})` to `printf("\n")`, fixed missing closing comment `/*creates an array...`

12. **Page 102**: Fixed garbled `p\rightarrow s p=(i n t^{*})malloc p p>r o w^{*}3^* sizeof (in` to proper malloc syntax, fixed `* (p-s p+2)=p\to r o w-1` to `*(p->sp + 2) = p->row - 1`, fixed `\mathbf{\nabla}^{*}` to `*(s.sp + i)`

13. **Page 103**: Fixed `void transpose (struct sparse ^*p struct sparse s )` to `void transpose(struct sparse *p, struct sparse s)`, fixed `\ ^{*}\left(\mathsf{p}\to\mathsf{s p}+\mathsf{p o s}_{\_2}\right)=\mathbf^{*}` to proper C syntax

14. **Page 104**: Fixed `Output:` to proper code block marker

15. **Page 105**: Fixed `^{*}(p\rightarrow s p+1)={}^{*}\left(s.s p+0\right)` to `*(p->sp + 1) = *(s.sp + 0)`

16. **Page 106**: Fixed `q=y^{*}3+1` to `q = y * 3 + 1`, `q=y^{+}3+1` to same, `pos2=x^{2}3+0` to `pos_2 = x * 3 + 0`, `pos2=x^{3}3+1` to `pos_2 = x * 3 + 1`, `\cos\ 2=x^{+}3+2` to `pos_2 = x * 3 + 2`

17. **Page 107**: Fixed `void addmat (struct sparse \ {*,,}struct sparse,struct sparse )` to `void addmat(struct sparse *, struct sparse, struct sparse)`

18. **Page 108**: Fixed `p\rightarrow s p=(i n t^{*})malloc` to proper syntax, fixed `int ));` placement

19. **Page 109**: Fixed `int c n t=0,\;\for` to `int cnt = 0, i; for`

20. **Page 110**: Fixed `p-s p=(i n t^{}}malloc` to `p->sp = (int *)malloc`, fixed `\mathbf{\nabla}^{*}` to `*(s.sp + i)`

21. **Page 111**: Fixed `\ \ {\sf j}=\left({\sf\pi}^{*}\left({\sf\}.{\sf s}.{\\sf\ p}+2\right)*3\right)+3` to `j = (*(s.sp + 2) + 1) * 3`, fixed `for \left(\begin{matrix}` to proper for loop

22. **Page 112**: Fixed `void addmat (struct sparse ^*\ p pstruct sparse s1,struct sparse s2)` to `void addmat(struct sparse *p, struct sparse s1, struct sparse s2)`, fixed `v\mathsf{a l a}={mathbf\ \sigma}^{*}` to `vala = *(s1.sp + i * 3 + 2)`, fixed `bma=\div{(s2,s p+2)}` to `bmax = *(s2.sp + 2)`

23. **Page 114**: Fixed `*(s.result +0+2)` to `*(s.result + 2)`

24. **Page 115**: Fixed `poited` to `pointed`, `jth` to `jth` (proper formatting)

25. **Page 116**: Fixed `\ {bf j}^{t h}` to `jth`

26. **Page 117**: Fixed `linked` to `linked list` (incomplete sentence)

27. **Page 118**: Fixed `down \ t\ {the` to `down of the`

28. **Page 120**: Fixed `spare` to `sparse` in bullet (d), `linked` to `linked list`

29. **Page 121**: Fixed `spare` to `sparse` in question (c), `interview Q` artifact removed

30. **Page 122**: Fixed `parse` to proper parameter name, fixed `in` to `int` in `insert` function prototype