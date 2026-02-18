---
title: Heap Sort
weight: 14
---

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