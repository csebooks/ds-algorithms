---
title: Queue as a Linked-List
weight: 3
---

Queue can also be represented using a linked list. Linked lists do not have any restrictions on the number of elements it can hold. Space for the elements in a linked list is allocated dynamically, hence it can grow as long as there is enough memory available for dynamic allocation. Figure 6-4 shows the representation of a queue as a linked list.

**Figure 6-4: Representation of a queue as a linked list**

```
front → [34|•] → [12|•] → [53|•] → [61|NULL] ← rear
```

Let us now see a program that implements the queue as a linked list.

### Program 6-2: Implementation of queue as a linked list

```c
#include <stdio.h>
#include <stdlib.h>

struct node {
    int data;
    struct node *link;
};

struct queue {
    struct node *front;
    struct node *rear;
};

void initqueue(struct queue *);
void addq(struct queue *, int);
int delq(struct queue *);
void delqueue(struct queue *);

int main() {
    struct queue a;
    int n;
    
    initqueue(&a);
    addq(&a, 34);
    addq(&a, 12);
    addq(&a, 53);
    addq(&a, 61);
    
    n = delq(&a);
    if (n != NULL)
        printf("Item deleted: %d\n", n);
    
    n = delq(&a);
    if (n != NULL)
        printf("Item deleted: %d\n", n);
    
    n = delq(&a);
    if (n != NULL)
        printf("Item deleted: %d\n", n);
    
    delqueue(&a);
    return 0;
}

/* initialises data member */
void initqueue(struct queue *q) {
    q->front = q->rear = NULL;
}

/* adds an element to the queue */
void addq(struct queue *q, int item) {
    struct node *temp;
    temp = (struct node *)malloc(sizeof(struct node));
    if (temp == NULL) {
        printf("Queue is full\n");
        return;
    }
    temp->data = item;
    temp->link = NULL;
    if (q->front == NULL) {
        q->rear = q->front = temp;
        return;
    }
    q->rear->link = temp;
    q->rear = temp;
}

/* removes an element from the queue */
int delq(struct queue *q) {
    struct node *temp;
    int item;
    if (q->front == NULL) {
        printf("Queue is empty\n");
        return NULL;
    }
    item = q->front->data;
    temp = q->front;
    q->front = q->front->link;
    if (q->front == NULL)
        q->rear = NULL;
    free(temp);
    return item;
}

/* deallocates memory */
void delqueue(struct queue *q) {
    struct node *temp;
    if (q->front == NULL)
        return;
    while (q->front !=NULL) {
        temp = q->front;
        q->front = q->front->link;
        free(temp);
    }
    q->rear = NULL;
}
```

### Output:
```
Item deleted: 34
Item deleted: 12
Item deleted: 53
```

In this program the structure queue contains two elements front and rear, both are of the type pointers to structure node. To begin with, the queue is empty hence both front and rear are set to NULL.

The `addq()` function adds a new element at the rear end of the list. If the element added is the first element, then both front and rear are made to point to the new node. However, if the element added is not the first element, then only rear is made to point to the new node, whereas front continues to point to the first node in the list.

The `delq()` function removes an element from the list which is at the front end of the list. Removal of an element from the list actually deletes the node to which front is pointing. After deletion of a node, front is made to point to the next node that comes in the list, whereas rear continues to point to the last node in the list. If the deleted node was the last node (i.e., front becomes NULL), then rear is also set to NULL.

The function `delqueue()` is called before `main()` comes to an end. This is done because the memory allocated for the existing nodes in the list must be deallocated.

---