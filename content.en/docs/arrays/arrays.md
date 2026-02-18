---
title: Arrays
weight: 3
---

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