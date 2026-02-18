---
title: Linear Search
weight: 3
---

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