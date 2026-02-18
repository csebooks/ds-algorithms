---
title: Queue as an Array
weight: 2
---

Representing a queue as an array would have the same problem that we discussed in case of stack in Chapter 5. An array can store a fixed number of elements. Queue, on the other hand keeps on changing as we remove elements from the front end or add new elements at the rear end. Declaring an array with a maximum size would solve this problem. The maximum size should be large enough for a queue to expand or shrink. Let us now see a program that implements queue as an array.

### Program 6-1: Implementation of queue as an array

```c
#include <stdio.h>
#define MAX 10

struct queue {
    int arr[MAX];
    int front, rear;
};

void initq(struct queue *);
void addq(struct queue *, int);
int delq(struct queue *);

int main() {
    struct queue q;
    int n;
    
    initq(&q);
    addq(&q, 34);
    addq(&q, 12);
    addq(&q, 53);
    addq(&q, 61);
    
    n = delq(&q);
    if (n != NULL)
        printf("Item deleted: %d\n", n);
    
    n = delq(&q);
    if (n != NULL)
        printf("Item deleted: %d\n", n);
    
    n = delq(&q);
    if (n != NULL)
        printf("Item deleted: %d\n", n);
    
    n = delq(&q);
    if (n != NULL)
        printf("Item deleted: %d\n", n);
    
    n = delq(&q);
    if (n != NULL)
        printf("Item deleted: %d\n", n);
    
    return 0;
}

/* initializes the queue */
void initq(struct queue *pq) {
    pq->front = -1;
    pq->rear = -1;
}

/* adds an element to the queue */
void addq(struct queue *pq, int item) {
    if (pq->rear == MAX - 1) {
        printf("Queue is full\n");
        return;
    }
    pq->rear++;
    pq->arr[pq->rear] = item;
    if (pq->front == -1)
        pq->front = 0;
}

/* removes an element from the queue */
int delq(struct queue *pq) {
    int data;
    if (pq->front == -1) {
        printf("Queue is Empty\n");
        return NULL;
    }
    data = pq->arr[pq->front];
    pq->arr[pq->front] = 0;
    if (pq->front == pq->rear)
        pq->front = pq->rear = -1;
    else
        pq->front++;
    return data;
}
```

### Output:
```
Item deleted: 34
Item deleted: 12
Item deleted: 53
Item deleted: 61
Queue is Empty
```

Here we have declared a structure queue containing an array `arr` to store queue elements and variables `front` and `rear` to monitor the two ends of the queue. The initial values of front and rear are set to -1, through the function `initq()` to mark the queue as empty. The functions `addq()` and `delq()` are used to perform addition and deletion operations on the queue.

In `addq()` firstly it is ascertained whether an addition is possible or not. Since the array indexing begins with 0 the maximum number of elements that can be stored in the queue are `MAX - 1`. If these many elements are already present in the queue, then it is reported to be full. If an element can be added to the queue, then value of rear is incremented and the new item is stored in the array.

If the item being added to the queue is the first element (i.e., if variable front has a value -1) then as soon as the item is added to the queue front is set to 0 indicating that the queue is no longer empty.

The addition of an element to the queue is illustrated in Figure 6-2.

**Figure 6-2: Addition of an element to a queue**

```
Empty Queue: front = -1, rear = -1

Add 34:     [34]          front=0, rear=0
            ↑↑
            front rear

Add 12:     [34, 12]      front=0, rear=1
            ↑      ↑
            front  rear

Add 53:     [34, 12, 53]  front=0, rear=2
            ↑           ↑
            front       rear

Add 61:     [34, 12, 53, 61]  front=0, rear=3
            ↑               ↑
            front           rear
```

Let us now see how the `delq()` function works. Before deleting an element from the queue, it is first ascertained whether there are any elements available for deletion. If not, then the queue is reported as empty. Otherwise, an element is deleted from `arr[front]`.

Imagine a case where we add 10 elements to the queue. Value of rear would now be 9. Suppose we have not deleted any elements from the queue, then at this stage the value of front would be 0. Now suppose we go on deleting elements from the queue. When the tenth element is deleted, the queue would fall empty. To make sure that another attempt to delete should be met with an 'empty queue' message, front and rear both are reset to -1 to indicate emptiness of the queue.

The deletion of elements from a queue is illustrated in Figure 6-3.

**Figure 6-3: Deletion of elements from a queue**

```
Before Deletion:    [34, 12, 53, 61]    front=0, rear=3
                     ↑              ↑
                     front          rear

After Deletion:     [0, 12, 53, 61]     front=1, rear=3
                        ↑           ↑
                        front       rear

Before Deletion:    [0, 12, 53, 61]     front=1, rear=3
                        ↑           ↑
                        front       rear

After Deletion:     [0, 0, 53, 61]      front=2, rear=3
                           ↑        ↑
                           front    rear

Before Deletion:    [0, 0, 53, 61]      front=2, rear=3
                           ↑        ↑
                           front    rear

After Deletion:     [0, 0, 0, 61]       front=3, rear=3
                              ↑     ↑
                              front rear

Before Deletion:    [0, 0, 0, 61]       front=3, rear=3
                              ↑     ↑
                              front rear

After Deletion:     [0, 0, 0, 0]        front=-1, rear=-1 (Empty)
```

Our program has got one limitation. Suppose we go on adding elements to the queue till the entire array gets filled. At this stage the value of rear would be `MAX - 1`. Now if we delete 5 elements from the queue, at the end of these deletions the value of front would be 5. If now we attempt to add a new element to the queue, then it would be reported as full even though in reality the first five slots of the queue are empty. To overcome this situation, we can implement a queue as a **circular queue**, which would be discussed later in this chapter.

---