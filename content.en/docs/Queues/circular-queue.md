---
title: Circular Queue
weight: 4
---

The queue that we implemented using an array suffers from one limitation. In that implementation there is a possibility that the queue is reported as full (since rear has reached the end of the array), even though in actuality there might be empty slots at the beginning of the queue.

To overcome this limitation, we can implement the queue as a **circular queue**. Here as we go on adding elements to the queue and reach the end of the array, the next element is stored in the first slot of the array (provided it is free).

More clearly, suppose an array `arr` of n elements is used to implement a circular queue. As we go on adding elements to the queue we will reach `arr[n-1]`. We cannot add any more elements to the queue as we have reached the end of the array. If some elements in the queue are deleted the slots at the beginning of the queue will fall vacant. If now any new elements are to be added to the queue, instead of reporting that the queue is full we fill the slots at the beginning of the array with new elements being added to the queue.

In short, just because we have reached the end of the array the queue would not be reported as full. The queue would be reported as full only when all the slots in the array stand occupied.

Let us now see a program that performs the addition and deletion operation on a circular queue.

### Program 6-3: Implementation of circular queue

```c
#include <stdio.h>
#define MAX 8

struct queue {
    int arr[MAX];
    int front, rear;
};

void initq(struct queue *);
void addq(struct queue *, int);
int delq(struct queue *);
void display(struct queue *);

int main() {
    struct queue q;
    int n;
    
    /* initialise circular queue */
    initq(&q);
    addq(&q, 14);
    addq(&q, 22);
    addq(&q, 13);
    addq(&q, -6);
    addq(&q, 25);
    addq(&q, 21);
    addq(&q, 17);
    addq(&q, 18);
    
    printf("Elements in the circular queue:\n");
    display(&q);
    
    n = delq(&q);
    if (n != NULL)
        printf("Item deleted: %d\n", n);
    
    n = delq(&q);
    if (n != NULL)
        printf("Item deleted: %d\n", n);
    
    printf("Elements in the circular queue after deletion:\n");
    display(&q);
    
    addq(&q, 9);
    addq(&q, 20);
    
    printf("Elements in the circular queue after addition:\n");
    display(&q);
    
    return 0;
}

/* initializes an empty queue */
void initq(struct queue *pq) {
    int i;
    pq->front = pq->rear = -1;
    for (i = 0; i < MAX; i++)
        pq->arr[i] = 0;
}

/* adds an element to the queue */
void addq(struct queue *pq, int item) {
    if ((pq->rear == MAX - 1 && pq->front == 0) ||
        (pq->rear + 1 == pq->front)) {
        printf("Queue is full\n");
        return;
    }
    if (pq->rear == MAX - 1)
        pq->rear = 0;
    else
        pq->rear++;
    pq->arr[pq->rear] = item;
    if (pq->front == -1)
        pq->front = 0;
}

/* removes an element from the queue */
int delq(struct queue *pq) {
    int data;
    if (pq->front == -1) {
        printf("Queue is empty\n");
        return NULL;
    }
    data = pq->arr[pq->front];
    pq->arr[pq->front] = 0;
    if (pq->front == pq->rear) {
        pq->front = -1;
        pq->rear = -1;
    }
    else {
        if (pq->front == MAX - 1)
            pq->front = 0;
        else
            pq->front++;
    }
    return data;
}

/* displays element in a queue */
void display(struct queue *pq) {
    int i;
    for (i = 0; i < MAX; i++)
        printf("%d\t", pq->arr[i]);
    printf("\n");
}
```

### Output:
```
Elements in the circular queue:
14	22	13	-6	25	21	17	18	
Item deleted: 14
Item deleted: 22
Elements in the circular queue after deletion:
0	0	13	-6	25	21	17	18	
Elements in the circular queue after addition:
9	20	13	-6	25	21	17	18	
```

Here the array `arr` is used to store the elements of the circular queue. The functions `addq()` and `delq()` are used to add and remove the elements from the queue respectively. The function `display()` displays the existing elements of the queue. The initial values of front and rear are set to -1, to mark the queue as empty.

In `main()`, first we have called the `addq()` function 8 times to insert elements in the circular queue. In this function, following cases are considered before adding an element to the queue:

(a) First, we have checked whether or not the array is full. The message 'Queue is full' gets displayed if front and rear are in adjacent locations with rear following the front.

(b) If the value of front is -1 then it indicates that the queue is empty and the element to be added would be the first element in the queue. The values of front and rear in such a case are set to 0 and the new element gets placed at the 0th position.

(c) It may also happen that some of the positions at the front end of the array are vacant. This happens if we have deleted some elements from the queue, when the value of rear is `MAX - 1` and the value of front is greater than 0. In such a case the value of rear is set to 0 and the element to be added is added at this position.

(d) The element is added at the rear position in case the value of front is either equal to or greater than 0 and the value of rear is less than `MAX - 1`.

Thus, after adding 8 elements the value of front and rear become 0 and 7 respectively. The `display()` function displays the elements in the queue. Figure 6-5 shows the circular queue after adding 8 elements.

**Figure 6-5: Circular queue after addition of 8 elements**

```
        rear
          ↓
    ┌─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┐
    │ 17  │ 18  │ 14  │ 22  │ 13  │ -6  │ 25  │ 21  │
    └─────┴─────┴─────┴─────┴─────┴─────┴─────┴─────┘
                      ↑
                    front

front = 0, rear = 7
```

Next we have called `delq()` function twice to remove 2 elements from the queue. The following conditions are checked while deleting an element:

(a) First, we have checked whether or not the queue is empty. The value of front in our case is 0, hence an element at the front position would get deleted.

(b) Next, we have checked if the value of front has become equal to rear. If it has, then the element we wish to remove is the only element of the queue. On removal of this element the queue would become empty and hence the values of front and rear are set to -1.

On deleting an element from the queue, the value of front is set to 0 if it is equal to `MAX - 1`. Otherwise, front is simply incremented by 1. Figure 6-6 shows the circular queue after deleting two elements from the queue that was earlier filled with 8 elements.

**Figure 6-6: Circular queue after deleting two elements**

```
        rear
          ↓
    ┌─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┐
    │ 17  │ 18  │  0  │  0  │ 13  │ -6  │ 25  │ 21  │
    └─────┴─────┴─────┴─────┴─────┴─────┴─────┴─────┘
                                  ↑
                                front

front = 2, rear = 7
```

---