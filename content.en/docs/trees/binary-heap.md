---
title: Binary Heap
weight: 9
---

**Binary heap** is a **complete binary tree**. It means all its levels are completely filled except perhaps last and at the last level nodes are as much to left as possible.

There are two types of heaps:

| Type | Property |
|------|----------|
| **Max heap** (descending heap) | Value at any node is **greater** than all its children |
| **Min heap** (ascending heap) | Value at any node is **smaller** than all its children |

![Figure 7-17: Types of heaps](image-placeholder)

### Heapify Operation

One of the common operations carried out while using a binary heap is **heapification** of a node. While heapifying a node in a max heap, we need to ensure that all its children satisfy the heap property—**Parent >= Left child, Right child**.

**Steps:**
1. Pick maximum out of given node, and its left and right child
2. If maximum is root, do nothing
3. If maximum is left, exchange root with left and heapify left node
4. If maximum is right, exchange root with right and heapify right node

![Figure 7-18: Heapify operation](image-placeholder)

![Figure 7-19: Multi-step heapify operation](image-placeholder)

---

### Program 7-3: Construction of max heap

```c
#include <stdio.h>

void heapify(int [], int, int);

int main() {
    int arr[] = {11, 2, 9, 13, 3, 25, 17, 1, 90, 57};
    int i, size;
    size = 10;
    
    for (i = size / 2 - 1; i >= 0; i--)
        heapify(arr, size, i);
    
    for (i = 0; i < size; i++)
        printf("%d\t", arr[i]);
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

**Output:**
```
90	57	25	13	11	9	17	1	2	3	
```

On execution of the program the binary tree shown in Figure 7-20(a) gets converted into a max heap shown in Figure 7-20(b).

![Figure 7-20: Conversion of binary tree to max heap](image-placeholder)

### Applications of Binary Heap

- Finding minimum spanning tree
- Finding the shortest path in a network of cities
- Implementing priority queues
- Merging K sorted arrays

---

# Chapter Summary