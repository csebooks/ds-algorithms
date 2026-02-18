---
title: Recursive Binary Search
weight: 5
---

We have used a while loop to implement the binary search algorithm in Program 9-2. It is also possible to implement this algorithm using recursion. This recursive implementation is given below.

### Program 9-3: Implementation of Recursive Binary Search algorithm

```c
#include <stdio.h>

int recbinsearch(int [], int, int, int);

int main() {
    int arr[] = {1, 2, 3, 9, 11, 13, 17, 25, 57, 90};
    int num, pos;
    
    printf("Enter number to search: ");
    scanf("%d", &num);
    pos = recbinsearch(arr, num, 0, 9);
    if (pos == -1)
        printf("Number is not present in the array\n");
    else
        printf("Number is at position %d in the array\n", pos);
    
    return 0;
}

int recbinsearch(int a[], int num, int lower, int upper) {
    int mid;
    if (lower <= upper) {
        mid = (lower + upper) / 2;
        if (num == a[mid])
            return mid;
        if (num > a[mid])
            return recbinsearch(a, num, mid + 1, upper);
        if (num < a[mid])
            return recbinsearch(a, num, lower, mid - 1);
    }
    return -1;
}
```

In `recbinsearch()` we compare `num` with the middle element. If it matches with middle element, we return the index `mid`. Otherwise if `num` is found to be greater than the mid element, then `num` can only lie in right half subarray after the mid element. So we call `recbinsearch()` for right half of the array. Finally, if `num` is found to be smaller than the mid element, then `num` can only lie in left half subarray before the mid element. So we call `recbinsearch()` for left half of the array.

To find time complexity of recursive binary search algorithm, let us consider 3 cases shown in Figure 9-2.

**Figure 9-2: Progress of recursive Binary search**

```
Array: [1, 2, 3, 9, 11, 13, 17, 25, 57, 90]

Case (a): Search for num = 25
Iteration 1: lower=0, upper=9, mid=4 (value 11)
             25 > 11, search right half
Iteration 2: lower=5, upper=9, mid=7 (value 25)
             Match found! Position 7
             (3 comparisons)

Case (b): Search for num = 57
Iteration 1: lower=0, upper=9, mid=4 (value 11)
             57 > 11, search right half
Iteration 2: lower=5, upper=9, mid=7 (value 25)
             57 > 25, search right half
Iteration 3: lower=8, upper=9, mid=8 (value 57)
             Match found! Position 8
             (3 comparisons)

Case (c): Search for num = 100 (not present)
Iteration 1: lower=0, upper=9, mid=4 (value 11)
             100 > 11, search right half
Iteration 2: lower=5, upper=9, mid=7 (value 25)
             100 > 25, search right half
Iteration 3: lower=8, upper=9, mid=8 (value 57)
             100 > 57, search right half
Iteration 4: lower=9, upper=9, mid=9 (value 90)
             100 > 90, search right half
Iteration 5: lower=10, upper=9
             lower > upper, Search ends
             100 not found
             (4 comparisons)
```

In case (a) it takes 3 comparisons to search 57. In case (b) it takes 3 comparisons to search 25. Lastly, in case (c), it takes 4 comparisons to reach a conclusion that 100 is not present in the array. So, we can conclude that, in worst case, it does log₂ n comparisons. Note that value of log₂ 10 is between 3 and 4. To get exact number of comparisons the input array size must be a power of 2. We can safely conclude that the time complexity of recursive binary search algorithm is **O(log₂ n)**.

---