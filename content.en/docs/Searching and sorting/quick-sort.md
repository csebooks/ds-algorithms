---
title: Quick Sort
weight: 11
---

Quick sort is a very popular sorting method. It is also known as partition exchange sort. The basis of this algorithm is that it is faster and easier to sort two small arrays than one large array. Thus, the basic strategy of quick sort is to divide and conquer.

Consider a stack of papers each bearing name of a student and we wish to sort them by name. We can use the following approach. Pick a splitting value, say L (known as pivot element) and divide the stack of papers into two piles, A-L and M-Z (note that each pile may not contain the same number of papers). Then take the first pile and sub-divide it into two piles, A-F and G-L. The A-F pile can be further broken down into A-C and D-F. This division process goes on until the piles are small enough to be easily sorted. The same process is applied to the M-Z pile. Eventually, all the small sorted piles can be stacked one on top of the other to produce an ordered set of papers.

This strategy is based on recursion—on each attempt to sort the stack of papers, the pile is divided and then the same approach is used to sort each smaller pile (a smaller case).

The quick sort algorithm can be explained with the help of Figure 9-6. In this figure the element marked by '*' is the pivot element and the element marked by '—' is the element whose position is finalized.

**Figure 9-6: Quick sort**

```
Initial: [11*, 2, 9, 13, 57, 25, 17, 1, 90, 3]
          ↑
        (pivot = 11)

Step 1: Move from left (p) to find element > 11: found 13 at index 3
        Move from right (q) to find element < 11: found 3 at index 9
        Swap 13 and 3 → [11*, 2, 9, 3, 57, 25, 17, 1, 90, 13]

Step 2: Continue: p finds 57, q finds 1
        Swap 57 and 1 → [11*, 2, 9, 3, 1, 25, 17, 57, 90, 13]

Step 3: Continue: p finds 25, q finds 17
        Swap 25 and 17 → [11*, 2, 9, 3, 1, 17, 25, 57, 90, 13]

Step 4: Continue: p finds 25, q finds 17 (crossed)
        p > q, so stop. Swap pivot with element at q
        Swap 11 and 1 → [1, 2, 9, 3, 11—, 17, 25, 57, 90, 13]

Result: [1, 2, 9, 3] [11] [17, 25, 57, 90, 13]
        (left < 11)    (pivot) (right > 11)
        
Now recursively sort left and right sub-arrays
```

The array in Figure 9-6 consists of 10 elements. The quick sort algorithm works as follows:

(a) In the first iteration, we take the 0th element, i.e., 11, as a pivot element and place it at its final position such that all elements to the left of it are less than 11 and all elements to the right of it are greater than 11. To divide the array in this way we use two index variables, p and q.

(b) Using index variable p we move in the array from left to right in search of an element greater than 11. In our case p is incremented till we reach 13.

(c) Similarly, using q we move in the array from right to left in search of an element smaller than 11. In our case q is not decremented even once because 3 is less than 11.

(d) Now 13 and 3 are interchanged. Again, from their current positions p and q are incremented and decremented respectively and exchanges are made appropriately if desired.

(e) The process ends when p exceeds q. In our case, this happens when p reaches 25 and q reaches 1.

(f) Now, the 0th element 11 is interchanged with the value at index q, i.e., 1.

(g) The array is thus divided into two sub-arrays—elements to the left of 11 and elements to the right of 11, with 11 at its final position.

(h) Now the same procedure is applied to the two sub-arrays and then to the sub-arrays of these sub-arrays. As a result, at the end when all sub-arrays contain only one element, the original array gets sorted.

Note that it is not necessary that the pivot element must be the 0th element. We can choose any other element as pivot. The program given below implements the quick sort algorithm.

### Program 9-7: Implementation of Quick Sort algorithm

```c
#include <stdio.h>

void quicksort(int [], int, int);
int split(int [], int, int);

int main() {
    int arr[] = {11, 2, 9, 13, 57, 25, 17, 1, 90, 3};
    int i;
    
    printf("Quick sort\n");
    printf("Array before sorting:\n");
    for (i = 0; i < 10; i++)
        printf("%d\t", arr[i]);
    
    quicksort(arr, 0, 9);
    
    printf("\nArray after sorting:\n");
    for (i = 0; i < 10; i++)
        printf("%d\t", arr[i]);
    
    return 0;
}

void quicksort(int a[], int lower, int upper) {
    int i;
    if (upper > lower) {
        i = split(a, lower, upper);
        quicksort(a, lower, i - 1);
        quicksort(a, i + 1, upper);
    }
}

int split(int a[], int lower, int upper) {
    int p, q, num, temp;
    p = lower + 1;
    q = upper;
    num = a[lower];
    
    while (q >= p) {
        while (a[p] < num)
            p++;
        while (a[q] > num)
            q--;
        if (q > p) {
            temp = a[p];
            a[p] = a[q];
            a[q] = temp;
        }
    }
    
    temp = a[lower];
    a[lower] = a[q];
    a[q] = temp;
    return q;
}
```

### Output:
```
Quick sort
Array before sorting:
11	2	9	13	57	25	17	1	90	3	
Array after sorting:
1	2	3	9	11	13	17	25	57	90	
```

The first and last indexes passed to `quicksort()` reflect the part of the array that is being currently processed. In the first call we pass 0 and 9, since there are 10 integers in our array.

In the function `quicksort()`, a condition is checked whether `upper` is greater than `lower`. If the condition is satisfied then only the array will be split into two parts, otherwise, the control will simply be returned. To split the array into two parts the function `split()` is called.

In the function `split()`, to start with the two variables p and q are assigned the values `lower + 1` and `upper`. Then a while loop is executed that checks whether the indexes p and q have crossed each other. If they haven't then inside the while loop two more nested while loops are executed to increase the index p and decrease the index q. Then it is checked whether q is greater than p. If so, then the elements present at pth and qth positions are interchanged.

Finally, when the control returns to the function `quicksort()` two recursive calls are made to function `quicksort()`. This is done to sort the two split sub-arrays. As a result, after all the recursive calls when the control reaches the function `main()` the array becomes sorted.

In quick sort we choose a pivot and then split the array into sub-arrays. Then we again choose a pivot element in each of these sub-arrays and further split them. The best case in quick sort would be when we always choose the middle element of the array as the pivot element. Suppose to reach a sub-array of 1 element we have to do k iterations.

Then, n/2^k = 1

Taking log of both sides we get,

log₂ 2^k = log₂ n

Therefore, k = log₂ n.

In each of these k iterations for splitting the array we have to do n comparisons. Hence the total number of comparisons in quick sort will be n * log₂ n. So time complexity of quick sort in best case is **O(n log₂ n)**.

The worst case in quick sort will occur when the input is an array which is already sorted. In this case if we take the first element as pivot then there won't be any left sub-array. Except the pivot, all elements will be in right sub-array. Same thing will happen at each level. So while splitting there will be n comparisons at level 1, n-1 comparison at level 2, n-2 comparisons at level 3, etc. So totally there will be n*(n+1)/2 comparisons. So time complexity will be **O(n²)**.

---