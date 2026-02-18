---
title: Selection Sort
weight: 9
---

This is perhaps the simplest method of sorting. In this method, to sort the data in ascending order, the 0th element is compared with all other elements. If the 0th element is found to be greater than the compared element then they are interchanged. So, after the first iteration the smallest element gets placed at the 0th position. The same procedure is repeated for the 1st element and so on. This procedure can be best understood with the help of Figure 9-4.

**Figure 9-4: Selection sort at work**

```
Initial: [25, 17, 31, 13, 2]

First Iteration (find minimum for position 0):
  Compare 25 & 17: 25 > 17, swap → [17, 25, 31, 13, 2]
  Compare 17 & 31: 17 < 31, no swap → [17, 25, 31, 13, 2]
  Compare 17 & 13: 17 > 13, swap → [13, 25, 31, 17, 2]
  Compare 13 & 2: 13 > 2, swap → [2, 25, 31, 17, 13]
  (2 is now at position 0)

Second Iteration (find minimum for position 1):
  Compare 25 & 31: 25 < 31, no swap → [2, 25, 31, 17, 13]
  Compare 25 & 17: 25 > 17, swap → [2, 17, 31, 25, 13]
  Compare 17 & 13: 17 > 13, swap → [2, 13, 31, 25, 17]
  (13 is now at position 1)

Third Iteration (find minimum for position 2):
  Compare 31 & 25: 31 > 25, swap → [2, 13, 25, 31, 17]
  Compare 25 & 17: 25 > 17, swap → [2, 13, 17, 31, 25]
  (17 is now at position 2)

Fourth Iteration (find minimum for position 3):
  Compare 31 & 25: 31 > 25, swap → [2, 13, 17, 25, 31]
  (25 is now at position 3)

Sorted: [2, 13, 17, 25, 31]
```

Suppose an array `arr` consists of 5 numbers. The selection sort algorithm works as follows:

(a) In the first iteration the 0th element 25 is compared with 1st element 17 and since 25 is greater than 17, they are interchanged.

(b) Now the 0th element 17 is compared with 2nd element 31. But 17 is less than 31, so they are not interchanged.

(c) This process is repeated till 0th element is compared with rest of the elements and interchanged if necessary.

(d) At the end of the first iteration, the 0th element is the smallest element.

(e) Now the second iteration starts with the 1st element 25. The above process of comparison and swapping is repeated.

(f) So, if there are n elements in the array, then after (n-1) iterations the array is sorted.

The following program sorts the given list using selection sort algorithm.

### Program 9-5: Implementation of Selection Sort algorithm

```c
#include <stdio.h>

void selectionsort(int [], int);

int main() {
    int arr[] = {25, 17, 31, 13, 2};
    int i;
    
    printf("Selection sort\n");
    printf("Array before sorting:\n");
    for (i = 0; i < 5; i++)
        printf("%d\t", arr[i]);
    
    selectionsort(arr, 5);
    
    printf("\nArray after sorting:\n");
    for (i = 0; i < 5; i++)
        printf("%d\t", arr[i]);
    
    return 0;
}

void selectionsort(int a[], int size) {
    int i, j, temp;
    for (i = 0; i < size - 1; i++) {
        for (j = i + 1; j < size; j++) {
            if (a[i] > a[j]) {
                temp = a[i];
                a[i] = a[j];
                a[j] = temp;
            }
        }
    }
}
```

### Output:
```
Selection sort
Array before sorting:
25	17	31	13	2	
Array after sorting:
2	13	17	25	31	
```

Here, `a[i]` is compared with `a[j]`. If the element `a[i]` is found to be greater than `a[j]` then they are interchanged. The value of j is starting from `i+1`, as we need to compare any element with all elements following it.

When the array has 5 elements the number of comparisons made in each iteration will be as follows:
- 1st iteration - 4 comparisons
- 2nd iteration - 3 comparisons
- 3rd iteration - 2 comparisons
- 4th iteration - 1 comparison

So, in general, for an array of n elements the number of comparisons will be n(n-1)/2. So time complexity of selection sort algorithm is **O(n²)**.

---