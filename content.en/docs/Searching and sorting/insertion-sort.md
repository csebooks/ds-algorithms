---
title: Insertion Sort
weight: 10
---

This algorithm works by inserting each element at an appropriate position in the array. The array is divided into two sets—one contains sorted values and another contains unsorted values. To begin with, the element at 0th position is in the sorted set and the rest are in the unsorted set. During each iteration, the first element in the unsorted set is picked up and inserted at the correct position in the sorted set. The correct position is determined by traversing the sorted set from right to left and comparing the picked element with the elements in the sorted set. During comparison if it is found that picked element can be inserted then space is created for it by shifting the other elements one position to the right. Let us understand this algorithm with the help of Figure 9-5.

**Figure 9-5: Insertion sort at work**

```
Initial: [25, 17, 31, 13, 2]
         ↑
       (sorted: [25], unsorted: [17, 31, 13, 2])

First Iteration (insert 17):
  Compare 17 with 25: 17 < 25, shift 25 right
  Insert 17 at position 0 → [17, 25, 31, 13, 2]

Second Iteration (insert 31):
  Compare 31 with 25: 31 > 25, no shift needed
  31 stays at position 2 → [17, 25, 31, 13, 2]

Third Iteration (insert 13):
  Compare 13 with 31: 13 < 31, shift 31 right → [17, 25, 31, 31, 2]
  Compare 13 with 25: 13 < 25, shift 25 right → [17, 25, 25, 31, 2]
  Compare 13 with 17: 13 < 17, shift 17 right → [17, 17, 25, 31, 2]
  Insert 13 at position 0 → [13, 17, 25, 31, 2]

Fourth Iteration (insert 2):
  Compare 2 with 31: 2 < 31, shift 31 right
  Compare 2 with 25: 2 < 25, shift 25 right
  Compare 2 with 17: 2 < 17, shift 17 right
  Compare 2 with 13: 2 < 13, shift 13 right
  Insert 2 at position 0 → [2, 13, 17, 25, 31]

Sorted: [2, 13, 17, 25, 31]
```

Given below is the explanation of insertion sort algorithm for an array of 5 elements shown in Figure 9-5:

(a) In the first iteration the 1st element 17 is compared with the 0th element 25. Since 17 is smaller than 25, 17 is inserted at 0th place. Before that the 0th element 25 is shifted one position to the right.

(b) In the second iteration, the 2nd element 31 is compared with element before it, i.e., 25. Since 31 is greater than 25, nothing is done as 31 is at its correct position.

(c) In the third iteration, the 3rd element 13 is compared successively with 31, 25, and 17. Since, 13 is smaller than all of them, they are shifted to right by one position and then 13 is inserted.

(d) In the fourth iteration the 4th element 2 is compared with elements 31, 25, 17 and 13. Since, 2 is smaller than all of them, these elements are shifted to right by one position and then 2 is inserted.

At the end of 4th iteration, the array becomes a sorted array. The following program implements the insertion sort algorithm.

### Program 9-6: Implementation of Insertion Sort algorithm

```c
#include <stdio.h>

void insertionsort(int [], int);

int main() {
    int arr[] = {25, 17, 31, 13, 2};
    int i;
    
    printf("Insertion sort\n");
    printf("Array before sorting:\n");
    for (i = 0; i < 5; i++)
        printf("%d\t", arr[i]);
    
    insertionsort(arr, 5);
    
    printf("\nArray after sorting:\n");
    for (i = 0; i < 5; i++)
        printf("%d\t", arr[i]);
    
    return 0;
}

void insertionsort(int a[], int size) {
    int i, j, temp;
    for (i = 1; i < size; i++) {
        temp = a[i];
        j = i - 1;
        while (j >= 0 && a[j] > temp) {
            a[j + 1] = a[j];
            j--;
        }
        a[j + 1] = temp;
    }
}
```

### Output:
```
Insertion sort
Array before sorting:
25	17	31	13	2	
Array after sorting:
2	13	17	25	31	
```

In the program the outer for loop is starting from 1 as the unsorted set starts at 1st position. The inner loop is used for comparison to decide the position where the picked element (`temp`) should be inserted and for shifting the elements one position to the right to make room for inserting the picked element.

Let us consider best case and worst case for analyzing the time complexity of this algorithm. The best case is when the array is already sorted and the worst case is when the array elements are in descending order. The important operations to be considered in this algorithm are comparison to determine where the element should be inserted and movement to create space for inserting the element.

In the best case the number of comparisons and movements will be as shown below.
- for i = 1, 1 comparison + 0 movement = 1
- for i = 2, 1 comparison + 0 movement = 1
- for i = 3, 1 comparison + 0 movement = 1
- for i = 4, 1 comparison + 0 movement = 1
- ... for i = n, 1 comparison + 0 movement = 1

So total number of operations will be 1 + 1 + 1 + 1.... This sum will be equal to n. Thus time complexity in best case will be **O(n)**.

In the worst case the number of comparisons and movements will be as shown below.
- for i = 2, 1 comparison + 1 movement = 2
- for i = 3, 2 comparisons + 2 movements = 4
- for i = 4, 3 comparisons + 3 movements = 6
- for i = n, (n-1) comparisons + (n-1) movements = 2(n-1)

If we add all this, we get
```
2 + 4 + 6 + 8 + ... + 2(n-1)
= 2(1 + 2 + 3 + 4 + ... + (n-1))
= 2(n(n-1)/2)
= O(n²)
```

Thus time complexity in worst case will be **O(n²)**.

---