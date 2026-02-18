---
title: Merge Sort
weight: 13
---

Like Quick sort, Merge sort is also a recursive algorithm. It goes on splitting the array into sub-arrays till we get sub-arrays of size 1. Then it compares elements of 1-element sub-arrays to merge them into a 2-element sorted array. Then it merges two such 2-element sorted sub-arrays to build a 4-element sorted sub-array. This process continues up the ladder till we get a complete sorted array.

This merging process for two 5-element sorted sub-arrays is shown in Figure 9-8. In the first step elements 2 and 1 are compared. Of these, 1 is smaller. Hence it is transferred to the sorted array. Then 2 and 3 are compared, and so on.

Note that, if during comparison end of one of the sub-arrays is reached, then the remaining elements from the other sub-array are copied into the third array.

**Figure 9-8: Merge sort at work**

```
Sub-array 1: [2, 9, 11, 13, 57]
Sub-array 2: [1, 3, 17, 25, 90]

Step 1:  Compare 2 and 1, 1 is smaller → [1]
Step 2:  Compare 2 and 3, 2 is smaller → [1, 2]
Step 3:  Compare 9 and 3, 3 is smaller → [1, 2, 3]
Step 4:  Compare 9 and 17, 9 is smaller → [1, 2, 3, 9]
Step 5:  Compare 11 and 17, 11 is smaller → [1, 2, 3, 9, 11]
Step 6:  Compare 13 and 17, 13 is smaller → [1, 2, 3, 9, 11, 13]
Step 7:  Compare 57 and 17, 17 is smaller → [1, 2, 3, 9, 11, 13, 17]
Step 8:  Compare 57 and 25, 25 is smaller → [1, 2, 3, 9, 11, 13, 17, 25]
Step 9:  Compare 57 and 90, 57 is smaller → [1, 2, 3, 9, 11, 13, 17, 25, 57]
Step 10: Sub-array 1 exhausted, copy remaining from sub-array 2 → [1, 2, 3, 9, 11, 13, 17, 25, 57, 90]

Final sorted array: [1, 2, 3, 9, 11, 13, 17, 25, 57, 90]
```

The following program implements the merge sort algorithm.

### Program 9-9: Implementation of Merge Sort algorithm

```c
#include <stdio.h>
#include <stdlib.h>

void mergesort(int [], int, int);
void merge(int [], int, int, int);

int main() {
    int arr[] = {11, 2, 9, 13, 57, 25, 17, 1, 90, 3};
    int i;
    
    printf("Merge sort\n");
    printf("Array before sorting:\n");
    for (i = 0; i < 10; i++)
        printf("%d\t", arr[i]);
    
    mergesort(arr, 0, 9);
    
    printf("\nArray after sorting:\n");
    for (i = 0; i < 10; i++)
        printf("%d\t", arr[i]);
    
    return 0;
}

void mergesort(int arr[], int lower, int upper) {
    int mid;
    if (lower < upper) {
        mid = (lower + upper) / 2;
        mergesort(arr, lower, mid);
        mergesort(arr, mid + 1, upper);
        merge(arr, lower, mid, upper);
    }
}

void merge(int arr[], int lower, int mid, int upper) {
    int size, *b, first, second, idx, i;
    size = upper - lower + 1;
    b = (int *)malloc(size * sizeof(int));
    first = lower;
    second = mid + 1;
    idx = 0;
    
    while (first <= mid && second <= upper) {
        if (arr[first] <= arr[second]) {
            b[idx] = arr[first];
            first++;
            idx++;
        }
        else {
            b[idx] = arr[second];
            second++;
            idx++;
        }
    }
    
    while (first <= mid) {
        b[idx] = arr[first];
        idx++;
        first++;
    }
    
    while (second <= upper) {
        b[idx] = arr[second];
        idx++;
        second++;
    }
    
    idx = 0;
    for (i = lower; i <= upper; i++) {
        arr[i] = b[idx];
        idx++;
    }
    free(b);
}
```

### Output:
```
Merge sort
Array before sorting:
11	2	9	13	57	25	17	1	90	3	
Array after sorting:
1	2	3	9	11	13	17	25	57	90	
```

The logic of `merge()` function is similar to the polynomial addition logic discussed in Chapter 2. The two sub-arrays being merged are part of the original array `arr[]`. They are identified as two separate sub-arrays using `lower`, `mid` and `upper`. The first sub-array is from index `lower` to `mid`, and the second from `mid + 1` to `upper`. For the purpose of merging another array `b[]` is created dynamically. Once array `b[]` contains the sorted elements, they are copied back into original array `arr[]` and the memory occupied by `b[]` is deallocated.

Suppose `arr[]` is an 8-element array. At level 1 we will split it into sub-arrays—`arr[0]` to `arr[3]` and `arr[4]` to `arr[7]`. At the next level, we will split the first sub-array into two sub-sub-arrays—one from `arr[0]` to `arr[1]` and second from `arr[2]` to `arr[3]`. So how many levels would we have if we are to reach 1-element sub-arrays? Well, it would be log₂ 8, or in general log₂ n. At each level we are doing n comparisons for merging. So time complexity of merge sort algorithm would be **O(n log₂ n)**.

---