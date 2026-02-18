---
title: Binary Search
weight: 4
---

Binary search method is very fast and efficient. This method requires that the list of elements be in sorted order. In this method, to search an element we compare it with the element present at the center of the list. If it matches then the search is successful. Otherwise, the list is divided into two halves—one from 0th element to the center element (first half), and another from center element to the last element (second half). As a result, all the elements in first half are smaller than the center element, whereas, all the elements in second half are greater than the center element.

The searching will now proceed in first or second half depending upon whether the element is smaller or greater than the center element. Same process of comparing the required element with the center element and if not found then dividing the elements into two halves is repeated for the first half or second half. This procedure is repeated till the element is found or the division of half parts gives one element. Let us understand this with the help of Figure 9-1.

**Figure 9-1: Binary search**

```
arr[]: [1, 2, 3, 9, 11, 13, 17, 25, 57, 90]
                         ↑
                       (center)
        
Search for num = 57:

Step 1: Compare 57 with center element 11
        57 > 11, so search right half: [13, 17, 25, 57, 90]
        
Step 2: Compare 57 with center element 25
        57 > 25, so search right half: [57, 90]
        
Step 3: Compare 57 with center element 57
        Match found! Position 8
```

Suppose an array consists of 10 sorted numbers and 57 is the element that is to be searched. The binary search method when applied to this array works as follows:

(a) 57 is compared with the element present at the center of the list (i.e., 11). Since 57 is greater than 11, the searching is restricted only to the second half of the array.

(b) Now 57 is compared with the center element of the second half of array (i.e., 25). Here again 57 is greater than 25 so the searching now proceeds in the elements present between 25 and 90.

(c) This process is repeated till 57 is found or no further division of subarray is possible.

Following program implements the binary search algorithm.

### Program 9-2: Implementation of Binary Search algorithm

```c
#include <stdio.h>

int binarysearch(int [], int, int);

int main() {
    int arr[] = {1, 2, 3, 9, 11, 13, 17, 25, 57, 90};
    int num, pos;
    
    printf("Enter number to search: ");
    scanf("%d", &num);
    pos = binarysearch(arr, 10, num);
    if (pos == -1)
        printf("Number is not present in the array\n");
    else
        printf("Number is at position %d in the array\n", pos);
    
    return 0;
}

int binarysearch(int a[], int size, int num) {
    int lower, upper, mid;
    lower = 0;
    upper = size - 1;
    
    while (lower <= upper) {
        mid = (lower + upper) / 2;
        if (num == a[mid])
            return mid;
        if (num > a[mid])
            lower = mid + 1;
        if (num < a[mid])
            upper = mid - 1;
    }
    return -1;
}
```

### Output:
```
Enter number to search: 57
Number is at position 8 in the array
```

In 1st iteration the algorithm works with n elements
In 2nd iteration it works with n/2 elements
In 3rd iteration it works with (n/2)/2 elements
In 4th iteration it works with ((n/2)/2)/2 elements

This goes on till we reach an iteration where number of elements being worked upon becomes 1. Suppose k iterations would be required to reach input size of 1. Thus,

n/2^k = 1

Taking log of both sides we get,

log₂ 2^k = log₂ n

Therefore, k = log₂ n.

During each iteration maximum of 3 comparisons are done. Thus number of comparisons in binary search is limited to 3 * log₂ n. Ignoring the constant 3, the time complexity will be **O(log₂ n)**.

Thus, a binary search gives better performance than linear search. The disadvantage of binary search is that it works only on sorted lists. So, if searching is to be performed on an unsorted list, then linear search is the only option.

---