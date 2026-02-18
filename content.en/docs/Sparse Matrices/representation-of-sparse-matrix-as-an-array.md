---
title: Representation of Sparse Matrix as an Array
weight: 2
---

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