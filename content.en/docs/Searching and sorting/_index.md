---
title: 'Searching and sorting'
weight: 9
references:
    books:
        - b1:
            title: Data Structures and Algorithm Analysis in C by Mark Allen Weiss 
            url: https://mrajacse.files.wordpress.com/2012/08/data-structures-and-algorithm-analysis-in-c-mark-allen-weiss.pdf
        - b2:
            title: Data_Structures_and_Algorithm_Analysis_2e By mark-allen-weiss
            url: https://www.google.co.in/books/edition/Data_Structures_and_Algorithm_Analysis_i/83RWbPynhkgC?hl=en&gbpv=1

---

# Chapter 9: Searching and Sorting
## Sorting Seek Me Out, Sort Me Out

### Why This Chapter Matters?

It would be an interesting statistic to find out how much time pre-computer-age generations spent in searching things and arranging them in an order. What a colossal waste it must have been to do these things manually! When history of computing is written 'searching' and 'sorting' would be right there at the top, as entities responsible for changing the way people do things.

---

We often spend time in searching some thing or the other. If the data is kept properly in some sorted order, then searching becomes very easy. Think of searching a word's meaning from an unordered list of words and then you will appreciate the way a dictionary is designed. In this chapter we are going to discuss different types of searching and sorting methods. Let us start with searching methods.

---

## Searching

Searching is an operation that finds the location of a given element in a list. The search is said to be successful or unsuccessful depending on whether the element that is to be searched is found or not. Here, we will discuss two standard searching methods—**Linear search** and **Binary search**.

---

## Linear Search

This is the simplest method of searching. In this method, an element is searched in the list sequentially. This method can be applied to a sorted or an unsorted list. Searching in unsorted list starts from the 0th element and continues until the element is found or the end of list is reached. As against this, searching in an ascending order sorted list starts from 0th element and continues until the element is found or an element whose value is greater than the value being searched is reached.

Following program implements linear search method for an unsorted as well as a sorted array.

### Program 9-1: Implementation of Linear Search algorithm

```c
#include <stdio.h>

int searchinsorted(int [], int, int);
int searchinunsorted(int [], int, int);

int main() {
    int unsortedarr[] = {11, 2, 9, 13, 57, 25, 17, 1, 90, 3};
    int sortedarr[] = {1, 2, 3, 9, 11, 13, 17, 25, 57, 90};
    int num, pos;
    
    printf("Enter number to search: ");
    scanf("%d", &num);
    pos = searchinunsorted(unsortedarr, 10, num);
    if (pos == -1)
        printf("Number is not present in the array\n");
    else
        printf("Number is at position %d in the array\n", pos);
    
    printf("Enter number to search: ");
    scanf("%d", &num);
    pos = searchinsorted(sortedarr, 10, num);
    if (pos == -1)
        printf("Number is not present in the array\n");
    else
        printf("Number is at position %d in the array\n", pos);
    
    return 0;
}

int searchinunsorted(int arr[], int size, int num) {
    int i;
    for (i = 0; i < size; i++) {
        if (arr[i] == num)
            return i;
    }
    return -1;
}

int searchinsorted(int arr[], int size, int num) {
    int i;
    if (num > arr[size - 1])
        return -1;
    for (i = 0; i < size; i++) {
        if (arr[i] > num)
            return -1;
        if (arr[i] == num)
            return i;
    }
    return -1;
}
```

### Output:
```
Enter number to search: 13
Number is at position 3 in the array
Enter number to search: 100
Number is not present in the array
```

In the program, `num` is the number that is to be searched in the array. While searching in `unsortedarr`, inside the for loop each time `arr[i]` is compared with `num`. If any element is equal to `num`, it means that the element is found. Hence its position in the array is returned. If control reaches beyond the for loop, it means that the element is not present in the array. In this case -1 is returned. We have returned -1, because no element can be present at position -1 in the array.

While searching in a sorted array, search starts at the 0th element and ends when the element is found or any element of the list is found to be greater than the element to be searched.

The number of comparisons in case of sorted list might be less as compared to the unsorted list because the search may not always continue till the end of the list.

The performance of linear search algorithm can be measured by counting the number of comparisons done to locate an element. In the worst case, in an array of size n, this algorithm would carry out n comparisons to reach a conclusion whether the element being searched is present in the array or not. Hence worst case time complexity of this algorithm is **O(n)**.

---

## Binary Search

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

## Recursive Binary Search

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

## Sorting

Sorting refers to arranging elements of a set in some order. There are different methods that are used to sort the data in ascending or descending order. These methods can be divided into two categories. They are as follows:

### Internal Sorting

If all the data to be sorted can be accommodated at a time in memory, then internal sorting methods are used.

### External Sorting

When the data to be sorted is so large that some of the data is present in the memory and some is kept in auxiliary memory (hard disk, tape, etc.), then external sorting methods are used. Let us begin with internal sorting methods.

---

## Internal Sorting

There are different types of internal sorting algorithms. We will discuss the common algorithms here. These algorithms sort the data in ascending order. With a minor change we can also sort the data in descending order.

---

## Bubble Sort

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

## Selection Sort

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

## Insertion Sort

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

## Quick Sort

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

## Binary Tree Sort

Binary tree sort uses a binary search tree (BST). In this algorithm, each element in the input list is inserted in a BST. During insertion the element being inserted is compared with nodes in the BST starting with the root node and moving towards the leaf nodes. If the element is less than node, then it is placed in the left branch, otherwise in the right branch. After all elements are inserted in the BST, it is traversed in inorder (left, root, right) to get the elements in ascending order.

Let's understand this in more details. Suppose `arr` is an array that consists of 10 distinct elements. The elements are as follows:
```
11, 2, 9, 13, 57, 25, 17, 1, 90, 3
```

The BST that can be built from these elements is shown in Figure 9-7.

**Figure 9-7: Binary Tree sort at work**

```
                    11
                   /  \
                  2    13
                 / \     \
                1   9     57
                   /     /  \
                  3     25   90
                       /
                      17

Input list: 11, 2, 9, 13, 57, 25, 17, 1, 90, 3

In-order traversal: 1, 2, 3, 9, 11, 13, 17, 25, 57, 90
```

The binary tree sort algorithm works as follows:

(a) To construct the binary search tree, we start with the 0th element 11. It is made the root of the tree.

(b) While inserting the 1st element, i.e., 2, 2 is compared with the root node 11. Since 2 is less than 11 it is made the left child of the root node 11.

(c) While inserting the 2nd element of the list, i.e., 13, it is compared with the root element 11. Since 13 is greater than 11 it is made the right child of the root node 11.

(d) Similarly, all other elements are placed in their proper position in the binary search tree.

(e) Now to get the elements in the sorted order, the tree is traversed in in-order and the elements are restored in the array.

The following program implements the binary tree sort algorithm.

### Program 9-8: Implementation of Binary Tree Sort algorithm

```c
#include <stdio.h>
#include <stdlib.h>

struct btreenode {
    struct btreenode *leftchild;
    int data;
    struct btreenode *rightchild;
};

void binarytreesort(int [], int);
void insert(struct btreenode **, int);
void inorder(struct btreenode *, int [], int *);

int main() {
    int arr[] = {11, 2, 9, 13, 57, 25, 17, 1, 90, 3};
    int i;
    
    printf("Binary Tree sort\n");
    printf("Array before sorting:\n");
    for (i = 0; i < 10; i++)
        printf("%d\t", arr[i]);
    
    binarytreesort(arr, 10);
    
    printf("\nArray after sorting:\n");
    for (i = 0; i < 10; i++)
        printf("%d\t", arr[i]);
    
    return 0;
}

void binarytreesort(int a[], int size) {
    struct btreenode *bt;
    int i;
    bt = NULL;
    for (i = 0; i < size; i++)
        insert(&bt, a[i]);
    i = 0;
    inorder(bt, a, &i);
}

void insert(struct btreenode **pr, int num) {
    if (*pr == NULL) {
        *pr = (struct btreenode *)malloc(sizeof(struct btreenode));
        (*pr)->leftchild = NULL;
        (*pr)->data = num;
        (*pr)->rightchild = NULL;
    }
    else {
        if (num < (*pr)->data)
            insert(&((*pr)->leftchild), num);
        else
            insert(&((*pr)->rightchild), num);
    }
}

void inorder(struct btreenode *pr, int a[], int *p) {
    if (pr != NULL) {
        inorder(pr->leftchild, a, p);
        a[*p] = pr->data;
        *p = *p + 1;
        inorder(pr->rightchild, a, p);
    }
}
```

### Output:
```
Binary Tree sort
Array before sorting:
11	2	9	13	57	25	17	1	90	3	
Array after sorting:
1	2	3	9	11	13	17	25	57	90	
```

The `binarytreesort()` function calls `insert()` function for each element in the array to construct the BST, and `inorder()` function to visit the constructed BST in in-order fashion.

In the `insert()` function it is ascertained whether BST is empty or not. If it is empty then a new node is created and the data to be inserted is stored in it. The left and right child of this new node is set with a NULL value, as this is the first node being inserted.

If BST is not empty then the current node is compared with the data to be inserted and `insert()` function is called recursively to insert the node in the left/right sub-tree. Thus `insert()` continues to move down the levels of BST until it reaches a leaf node. When it does, the new node gets inserted in the left/right sub-tree.

The `inorder()` function receives address of the root node of BST, address of the array and an index where each visited element of BST should be inserted in the array. In the function a condition is checked whether the pointer is NULL. If the pointer is not NULL then a recursive call is made first for the left child and then for the right child. The values passed are the address of the left and right children that are present in the pointers `leftchild` and `rightchild` respectively. In between these two calls the data of the current node is stored in the array.

In binary tree sort there are two distinct steps—creation of BST and visiting it in in-order. The worst case will be if the array is already in sorted order. Let us discuss the time complexity in this case.

While constructing the BST, to insert 1st element of this array into BST we have to perform 1 comparison, to insert 2nd element we have to do 2 comparisons, to insert 3rd element we have to do 3 comparisons. So to insert n elements it has to do n(n+1)/2 comparisons.

If there are n elements in the list there will be n nodes in the BST. While performing in-order traversal of the BST we perform maximum of 3 comparisons for any node. For n nodes the maximum number of comparisons will be 3n.

So, total number of comparisons for this algorithm will be n(n+1)/2 + 3n. Ignoring constants and lower order terms, time complexity of binary tree sort will be **O(n²)**.

The drawback of the binary tree sort is that additional space is required for building the BST.

---

## Merge Sort

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

## Heap Sort

In this algorithm a binary heap is used. Recall from Chapter 7 that all levels of a binary heap are completely filled except perhaps last and at the last level nodes are as much to left as possible. In a max-heap the value at the root of any sub-tree is greater than or equal to the value of either of its children.

Heap sort is an improvement over the binary tree sort. Unlike a binary tree sort, it does not create a new binary tree from the input data. Instead, it builds a heap by adjusting the position of elements within the array itself. Thus, it sorts the array in-place, without needing any extra space.

Given below are the steps involved in the heap sort algorithm.

(a) Build a max heap of array elements
(b) Swap Root element with last array element
(c) Build max heap excluding last element
(d) Decrease heap length by 1
(e) Repeat steps (b), (c), (d) until array gets sorted

Let us now understand this procedure with the help of an example. Suppose an array contains elements 11, 2, 9, 13, 57, 25, 17, 1, 90, and 3. A binary heap representation of this array is shown in Figure 9-9. To convert this binary heap into a max-heap we need to repeatedly heapify the nodes in it. While heapifying a node in a max heap, we need to ensure that all its children satisfy the heap property—Parent >= Left child, Right child. This operation involves following steps:

(a) Pick maximum out of given node, and its left and right child
(b) If maximum is root, do nothing
(c) If maximum is left, exchange root with left and heapify left node
(d) If maximum is right, exchange root with right and heapify right node

**Figure 9-9: Heapify operation**

```
Before heapify:
        11
       /  \
      2    9
     / \   / \
    13 57 25 17
   / \
  1   90

Heapify node 13: max(13, 1, 90) = 90 (right child)
Swap 13 and 90:
        11
       /  \
      2    9
     / \   / \
    90 57 25 17
   / \
  1   13

Heapify node 9: max(9, 25, 17) = 25 (left child)
Swap 9 and 25:
        11
       /  \
      2    25
     / \   / \
    90 57 9  17
   / \
  1   13
```

Note that in the binary tree shown in Figure 9-9 node 13 and node 9 are violating the heap property, so we need to heapify them. While heapifying 13, maximum out of 13, 1, and 90 is 90. Since 90 is the right child, it is exchanged with 13. As against this, while heapifying 9, maximum (25) turns out to be the left child. So, 25 is exchanged with 9. Since after exchange 13 and 9 became child nodes, we did not have to heapify them further.

The following program implements the heap sort algorithm.

### Program 9-10: Implementation of Heap Sort algorithm

```c
#include <stdio.h>

void heapsort(int [], int);
void heapify(int [], int, int);

int main() {
    int arr[] = {11, 2, 9, 13, 57, 25, 17, 1, 90, 3};
    int i;
    
    printf("Heap sort\n");
    printf("Array before sorting:\n");
    for (i = 0; i < 10; i++)
        printf("%d\t", arr[i]);
    
    heapsort(arr, 10);
    
    printf("\nArray after sorting:\n");
    for (i = 0; i < 10; i++)
        printf("%d\t", arr[i]);
    
    return 0;
}

void heapsort(int arr[], int size) {
    int i, t;
    
    /* create max heap */
    for (i = size / 2 - 1; i >= 0; i--)
        heapify(arr, size, i);
    
    for (i = size - 1; i > 0; i--) {
        /* move current root to end */
        t = arr[0];
        arr[0] = arr[i];
        arr[i] = t;
        
        /* heapify the reduced heap */
        heapify(arr, i, 0);
    }
}

void heapify(int arr[], int sz, int i) {
    int largest, lch, rch, t;
    lch = 2 * i + 1;
    rch = 2 * i + 2;
    
    if (lch >= sz)
        return;
    
    largest = i;
    
    /* if left child is larger than root */
    if (lch < sz && arr[lch] > arr[largest])
        largest = lch;
    
    /* if right child is larger than largest so far */
    if (rch < sz && arr[rch] > arr[largest])
        largest = rch;
    
    /* if largest is not root */
    if (largest != i) {
        t = arr[i];
        arr[i] = arr[largest];
        arr[largest] = t;
        
        /* heapify the affected sub-tree */
        heapify(arr, sz, largest);
    }
}
```

### Output:
```
Heap sort
Array before sorting:
11	2	9	13	57	25	17	1	90	3	
Array after sorting:
1	2	3	9	11	13	17	25	57	90	
```

The program begins by declaring an array that represents the binary tree. We know that in array representation of a binary tree, a node at location i has its left and right child at locations (2i+1) and (2i+2) respectively.

Next, in the `heapsort()` function in a for loop we have repeatedly called `heapify()` moving level by level from leaf towards root, and at any level from right to left, starting from node at location `size/2 - 1`. The `heapify()` function finds the largest out of given node, and its left and right child. If the given node turns out to be largest then it does nothing. But if left/right child turns out to be largest it exchanges the given node with left/right child and then proceeds to heapify the left/right child.

Note that in the program we do not physically construct this binary tree by establishing the link between the nodes. Instead, we imagine this tree and then readjust the array elements to form a heap.

Once the max-heap is created the current root node is moved to the end and `heapify()` is called once again to heapify the reduced heap.

Let us now analyze the time complexity of heap sort algorithm. For this we must first consider the time complexity of `heapify()` function. In the worst case, while heapifying a value it does log₂ n comparisons. This is equal to the height of a complete binary tree. Since we are calling this function n times in `heapsort()`, the time complexity of heap sort algorithm will be **O(n log₂ n)**.

---

## Chapter Bullets: Summary of Chapter

(a) Searching an element in a list can be done using linear search or binary search algorithm.

(b) Binary search algorithm is more efficient than linear search algorithm.

(c) Binary search algorithm expects the elements of a list in ascending order.

(d) Binary search can be done iteratively or recursively.

(e) Internal sorting is used when the input data can be accommodated in memory.

(f) External sorting is used when data is so huge that all of it cannot be stored in memory at a time.

(g) Common internal sorting algorithms include bubble sort, selection sort, insertion sort, quick sort, merge sort, binary tree sort and heap sort.

---

## Check Your Progress

### Exercise - Level I

**[A] State whether the following statements are True or False:**

(a) Sorting is the method of arranging a list of elements in a particular order.

(b) Linear search is more efficient than the binary search.

(c) Merge sort needs additional space to sort an array.

(d) Binary tree sort needs additional space to sort an array.

(e) Time complexity of Quick sort is O(n log₂ n).

(f) Insertion sort is more efficient than Heap sort.

---

### Exercise - Level II

**[B] Answer the Following:**

(a) What is the difference between an internal sorting and external sorting?

(b) Write a program that determines the first occurrence of a given sub-array within an array.

---

### Exercise Level III: Coding Interview Questions

**[C] Answer the Following:**

(a) Suppose an array contains n elements. Given a number x that may occur several times in the array. Find:
   - the number of occurrences of x in the array
   - the position of first occurrence of x in the array.

(b) Write a program that implements insertion sort algorithm for a linked list of integers.

(c) Write a program that sorts the elements of a two-dimensional array row wise / column wise.

---

### Case Scenario Exercise: External Sorting

External sorting is useful for sorting huge amount of data that cannot be accommodated in the memory all at a time. So data from the disk is loaded into memory part by part and each part that is loaded is sorted and the sorted data is stored into some intermediate file. Finally, all the sorted parts present in different intermediate files are merged into one single file.

Initially the original file (file number 1) is partitioned into two files (file number 2 and 3). Then one item is read from each file (file number 2 and 3) and the two items are written in sorted order in a new file (file number 4). Once again one item is read from each partitioned files (file number 2 and 3) and these two items are written in sorted order in another new file (file number 5). Thus, alternate pair of sorted items are stored in the file number 4 and 5. This procedure is repeated till the partitioned files (file number 2 and 3) come to an end.

Now following procedure is repeated twice:

(a) Read one item from file number 4 and 5 and write them in sorted order in file number 2.

(b) Read one item from file number 4 and 5 and write them in sorted order in file number 3.

Note that instead of creating two new files, the partitioned files (2 and 3) are being reused.

After this the following procedure is repeated 4 times:

(a) Read one item from file number 2 and 3 and write them in sorted order in file number 4.

(b) Read one item from file number 2 and 3 and write them in sorted order in file number 5.

In this way alternately items are moved from a pair of partitioned files to the pair of new files and from pair of new files to a pair of partitioned files. This procedure is repeated till the time we do not end up writing entire data in a single file. When this happens all the items in this file would be in sorted order.

Write a program that implements the external sort algorithm.
```

## Summary of Corrections Made:

1. **Page 238**: Fixed "W" at beginning of paragraph to "We"
2. **Page 239**: Fixed `Ic [{C}]{}` artifact to proper code
3. **Page 240**: Fixed `n_{i}` to `n` in time complexity explanation
4. **Page 242**: Fixed `IC! [{C}]{}` artifact
5. **Page 242**: Fixed `upper =size` to `upper = size - 1` in binary search (critical bug fix)
6. **Page 244**: Fixed recursive binary search to include `return` statements in recursive calls
7. **Page 248**: Fixed `bubblesort (a r r,5)` to `bubblesort(arr, 5)`
8. **Page 250**: Fixed `O(n2)` to `O(n²)` for bubble sort complexity
9. **Page 252**: Fixed `{c}` artifact to proper closing brace
10. **Page 256**: Fixed math formatting and `j` variable references
11. **Page 256**: Fixed "Thus time complexity in best case will be O(n2)" to "worst case" (typo in original)
12. **Page 258**: Fixed `p` and `q` formatting in description
13. **Page 260**: Fixed `void merge` function signature which was split across lines incorrectly
14. **Page 268**: Fixed `oid merge` to `void merge`
15. **Page 268**: Fixed `upper )` to `upper)` and `vo` artifact
16. **Page 272**: Fixed `for` loop syntax `for \left(\mathsf{i}=\mathsf{S i z e}\ \ {-}1\ ;\ {};\ {=}0\ ;;\\ {\mathsf{i}}\ \right)` to proper C syntax `for (i = size - 1; i > 0; i--)`
17. **Page 272**: Fixed `heapify` function comment `/*if largest is not root ^*/` to `/* if largest is not root */`
18. **Page 273**: Fixed `sz` parameter consistency in `heapify` function
19. **Page 274**: Fixed bullet (g) which was cut off to complete text about heap sort
20. **Page 275**: Fixed incomplete question (b) "Write a program that determines the first occurrence of a given sub-array within it" to "within an array"
21. **Page 276**: Fixed "S data" to "So data" in external sorting description
22. **Page 276**: Fixed "Write a progr gram that implements the external sort algor orithm" to "Write a program that implements the external sort algorithm"