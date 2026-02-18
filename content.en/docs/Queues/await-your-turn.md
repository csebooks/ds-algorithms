---
title: Await Your Turn
weight: 1
---

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