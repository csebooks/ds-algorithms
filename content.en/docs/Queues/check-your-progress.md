---
title: Check Your Progress
weight: 8
---

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