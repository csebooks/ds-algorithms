---
title: 'Queues'
weight: 6
references:
    books:
        - b1:
            title: Data Structures and Algorithm Analysis in C by Mark Allen Weiss 
            url: https://mrajacse.files.wordpress.com/2012/08/data-structures-and-algorithm-analysis-in-c-mark-allen-weiss.pdf
        - b2:
            title: Data_Structures_and_Algorithm_Analysis_2e By mark-allen-weiss
            url: https://www.google.co.in/books/edition/Data_Structures_and_Algorithm_Analysis_i/83RWbPynhkgC?hl=en&gbpv=1

---

# Chapter 6: Queues
## Await Your Turn

### Why This Chapter Matters?

Whether it is a railway reservation counter, a movie theatre or print jobs submitted to a network printer there is only one way to bring order to chaos—form a queue. If you await your turn patiently, there is a more likelihood that you would get a better service. In a computer system too there are queues of tasks (programs) waiting for the printer, or for access to disk storage, or for usage of CPU, etc. Understand this chapter thoroughly to be able to implement queue data structures.

---

Queue is a linear data structure that permits insertion of new element at one end and deletion of an element at the other end. The end at which the deletion of an element takes place is called **front**, and the end at which insertion of a new element takes place is called **rear**.

The first element that gets added into the queue is the first one to get removed from the list. Hence, queue is also referred to as **first-in-first-out (FIFO)** list. The name 'queue' comes from the everyday use of the term. Consider a queue of people waiting at a bus stop. Each new person who comes takes his or her place at the end of the line, and when the bus arrives, the people at the front of the line board first. The first person in the line is the first person to leave it. Figure 6-1 gives a pictorial representation of a queue.

**Figure 6-1: Pictorial representation of a queue**

```
[34, 12, 53, 61, 9, 23, -8, 42]
 ↑                      ↑
front                  rear
```

In Figure 6-1, 34 is the first element and 42 is the last element added to the queue. Similarly, 34 will be the first element to get removed and 42 will be the last element to get removed from the queue.

Queue, being a linear data structure can be represented using either an array or a linked list. These implementations are discussed in following sections.

---

## Queue as an Array

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

## Queue as a Linked-List

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

## Circular Queue

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

## Deque

The word **deque** is a short form of **double-ended queue** and defines a data structure in which items can be added or deleted at either the front or rear end, but no changes can be made elsewhere in the list. Thus, a deque is a generalization of both a stack and a queue. Figure 6-7 shows the representation of a deque.

**Figure 6-7: Representation of a deque**

```
Insertion →  ┌─────┬─────┬─────┬─────┬─────┐  ← Insertion
Deletion  ←  │ 34  │ 12  │ 53  │ 61  │  9  │  → Deletion
             └─────┴─────┴─────┴─────┴─────┘
               ↑                       ↑
             front                   rear
```

There are two variations of a deque:
- **Input-restricted deque**: restricts the insertion of elements at one end only, but the deletion of elements can be done at both the ends of a queue.
- **Output-restricted deque**: restricts the deletion of elements at one end only, and allows insertion to be done at both the ends of a deque.

---

## Priority Queue

A **priority queue** is a collection of elements where the elements are stored according to their priority levels. The order in which the elements should get added or removed is decided by the priority of the element. Following rules are applied to maintain a priority queue:

(a) The element with a higher priority is processed before any element of lower priority.

(b) If there are elements with the same priority, then the element added first in the queue would get processed first.

Priority queues are used for implementing job scheduling by the operating system where jobs with higher priorities are to be processed first. Another application of priority queues is simulation systems where priority corresponds to event times.

---

## Chapter Bullets: Summary of Chapter

(a) Queue data structure is a **FIFO** list in which addition of new elements takes place at the rear end of the queue and deletion of existing elements takes place at its front end.

(b) Queue data structure can be implemented using an array or a linked list.

(c) If queue is implemented as a linked list, then addition operation is like adding a new node at the end of the linked list.

(d) If queue is implemented as a linked list, then deletion operation is like deleting an existing node from the beginning of the linked list.

(e) There exist special types of queues like **deque** and **priority queue**.

---

## Check Your Progress

### Exercise - Level I

**[A] Fill in the blanks:**

(a) For a queue built using an array and containing n elements, the value of front would be **_____** and rear would be **_____**.

(b) In a circular queue implemented using an array and holding 5 elements, if front is equal to 3 and rear is equal to 4, then the new element would get placed at **_____** position.

(c) A queue is called **_____** when addition as well as deletion of elements can take place at both the ends.

(d) An **_____** is a queue in which insertion of an element takes place at one end only but deletion occurs at both the ends.

(e) An **_____** is a queue in which insertion of an element takes place at both the ends but deletion occurs at one end only.

---

### Exercise - Level II

**[B] Choose the correct alternative for the following:**

(a) Queue is a
1. Linear data structure
2. Non-linear data structure
3. Both (1) and (2)
4. None of the above

(b) The end at which a new element gets added to a queue is called
1. front
2. rear
3. top
4. bottom

(c) The end from which an element gets removed from the queue is called
1. front
2. rear
3. top
4. bottom

**[C] Which of the following applications would be suitable for a queue.**

1. A program is to keep track of patients as they check into a clinic, assigning them to doctors on a first-come, first-served basis.
2. An inventory of parts is to be processed by part number.
3. A dictionary of words used by spelling checker is to be created.
4. Customers are to take numbers at a bakery and be served in order when their numbers come.

---

### Exercise Level III: Coding Interview Questions

**[D] Write programs for the following:**

(a) Write a program to represent a deque using a linked list. Also write functions to add and delete elements from the deque.

(b) Write a menu-driven program to simulate processing of batch jobs by a computer system. The scheduling of these jobs should be handled using a priority queue. The program should allow user to add or remove items from the queue. It should also display current status i.e., the total number of items in the queue.

(c) Write a program to copy one queue to another when the queue is implemented as a linked list.

---

### Case Scenario Exercise: Priority Queues

Suppose there are several jobs to be performed with each job having a priority value of 1, 2, 3, 4, etc. Write a program that receives the job descriptions and the priorities. Create as many queues as the number of priorities and queue up the jobs into appropriate queues. For example, suppose the priorities are 1, 2, 3, and 4 and the data to be entered is as follows:

```
ABC, 2, XYZ, 1, PQR, 1, RTZ, 3, CBZ, 2, QQQ, 3, XXX, 4, RRR, 1
```

Then arrange these jobs as shown below:
- Q1: XYZ, 1, PQR, 1, RRR, 1
- Q2: ABC, 2, CBZ, 2
- Q3: RTZ, 3, QQQ, 3
- Q4: XXX, 4

The order of processing should be: Q1, Q2, Q3, Q4. Write a program to simulate the above scenario.
```

## Summary of Corrections Made:

1. **Program 6-1**: Fixed incomplete sentence in introductory text ("to be able to implement" → "to be able to implement queue data structures")

2. **Program 6-2**: 
   - Added missing `#include <stdlib.h>` for `malloc()` and `free()`
   - Fixed `addq()` function: added missing `return` statement after "Queue is full" printf
   - Fixed `addq()` function: changed `q->rear = q->rear->link` to `q->rear = temp` (correct logic)
   - Fixed `delq()` function: added check to set `q->rear = NULL` when queue becomes empty
   - Fixed `delqueue()` function: added `q->rear = NULL` at the end

3. **Program 6-3**: 
   - Fixed typo in `main()`: `addq (8\ q,9)` → `addq(&q, 9)`
   - Fixed `display()` function: `printf ((n^{n}))` → `printf("\n")`

4. **Figure 6-6 description**: Changed "The value of front in our case is 7" to "The value of front in our case is 0" (to match the actual code execution where front starts at 0)

5. **Text corrections**: Fixed various incomplete sentences and formatting issues throughout the document