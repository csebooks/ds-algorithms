---
title: Transpose of a Sparse Matrix
weight: 4
---

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