---
title: Bubble Sort
weight: 8
---

In this method, firstly 0th and 1st elements are compared. If 0th element is found to be greater than the 1st element then they are interchanged. Next, the 1st element is compared with the 2nd element, if it is found to be greater, then they are interchanged. In the same way all the adjacent pairs of elements are compared and interchanged if required. At the end of this iteration the largest element gets placed at the last position.

Similarly, in the second iteration the comparisons are made till the last but one element and this time the second largest element gets placed at the second last position in the list.

Once all such iterations are completed the list becomes a sorted list. This can be easily understood with the help of Figure 9-3.

**Figure 9-3: Bubble sort at work**

```
Initial: [25, 17, 31, 13, 2]

First Iteration:
  Compare 25 & 17: 25 > 17, swap → [17, 25, 31, 13, 2]
  Compare 25 & 31: 25 < 31, no swap → [17, 25, 31, 13, 2]
  Compare 31 & 13: 31 > 13, swap → [17, 25, 13, 31, 2]
  Compare 31 & 2: 31 > 2, swap → [17, 25, 13, 2, 31]
  (31 is now in its final position)

Second Iteration:
  Compare 17 & 25: 17 < 25, no swap → [17, 25, 13, 2, 31]
  Compare 25 & 13: 25 > 13, swap → [17, 13, 25, 2, 31]
  Compare 25 & 2: 25 > 2, swap → [17, 13, 2, 25, 31]
  (25 is now in its final position)

Third Iteration:
  Compare 17 & 13: 17 > 13, swap → [13, 17, 2, 25, 31]
  Compare 17 & 2: 17 > 2, swap → [13, 2, 17, 25, 31]
  (17 is now in its final position)

Fourth Iteration:
  Compare 13 & 2: 13 > 2, swap → [2, 13, 17, 25, 31]
  (13 is now in its final position)

Sorted: [2, 13, 17, 25, 31]
```

Suppose an array `arr` consists of 5 numbers. The bubble sort algorithm works as follows:

(a) In the first iteration the 0th element 25 is compared with 1st element 17 and since 25 is greater than 17, they are interchanged.

(b) Now the 1st element 25 is compared with 2nd element 31. But 25 is less than 31, so they are not interchanged.

(c) This process is repeated until (n-2)nd element is compared with (n-1)th element and interchanged if required.

(d) At the end of the first iteration, the (n-1)th element holds the largest number.

(e) Now the second iteration starts with the 0th element 17. The above process of comparison and interchanging is repeated but this time the last comparison is made between (n-3)rd and (n-2)nd elements.

(f) If there are n elements in the array then (n-1) iterations need to be performed.

The following program implements the bubble sort algorithm.

### Program 9-4: Implementation of Bubble Sort algorithm

```c
#include <stdio.h>

void bubblesort(int [], int);

int main() {
    int arr[] = {25, 17, 31, 13, 2};
    int i;
    
    printf("Bubble sort\n");
    printf("Array before sorting:\n");
    for (i = 0; i < 5; i++)
        printf("%d\t", arr[i]);
    
    bubblesort(arr, 5);
    
    printf("\nArray after sorting:\n");
    for (i = 0; i < 5; i++)
        printf("%d\t", arr[i]);
    
    return 0;
}

void bubblesort(int a[], int size) {
    int i, j, temp;
    for (i = 0; i < size - 1; i++) {
        for (j = 0; j < size - i - 1; j++) {
            if (a[j] > a[j + 1]) {
                temp = a[j];
                a[j] = a[j + 1];
                a[j + 1] = temp;
            }
        }
    }
}
```

### Output:
```
Bubble sort
Array before sorting:
25	17	31	13	2	
Array after sorting:
2	13	17	25	31	
```

The elements compared in bubble sort are always adjacent. Hence each time the elements compared are `a[j]` and `a[j+1]`. If the element `a[j]` is found to be greater than `a[j+1]` then they are interchanged.

If we wish to arrange the numbers in descending order then we need to make a small change in the condition, as shown below:

```c
if (a[j] < a[j + 1]) {
    /* exchange a[j] with a[j+1] */
}
```

When the array has 5 elements the number of comparisons that would be made in each iteration would be as follows:
- 1st iteration - 4 comparisons
- 2nd iteration - 3 comparisons
- 3rd iteration - 2 comparisons
- 4th iteration - 1 comparison

So, in general, for an array of n elements the number of comparisons will be n(n-1)/2. So time complexity of bubble sort algorithm is **O(n²)**.

---