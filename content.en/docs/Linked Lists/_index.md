---
title: 'Linked Lists'
weight: 3
references:
    books:
        - b1:
            title: Data Structures and Algorithm Analysis in C by Mark Allen Weiss 
            url: https://mrajacse.files.wordpress.com/2012/08/data-structures-and-algorithm-analysis-in-c-mark-allen-weiss.pdf
        - b2:
            title: Data_Structures_and_Algorithm_Analysis_2e By mark-allen-weiss
            url: https://www.google.co.in/books/edition/Data_Structures_and_Algorithm_Analysis_i/83RWbPynhkgC?hl=en&gbpv=1

---
# Chapter 3: Linked Lists

> **Stay connected**

## Why This Chapter Matters?

United we stand, divided we fall! More united and connected we are, more is the flexibility and scalability. Same is true with linked lists. Linked lists are used at numerous places in Computer Science. The flexibility and performance they offer is worth the pain of learning.

---

## What is a Linked List?

While the elements of an array occupy contiguous memory locations, those of a linked list are not constrained to be stored in adjacent locations. The order of the elements is maintained by explicit links between them.

### Typical Node Structure

| data | link |
|:----:|:----:|

### Example Linked List
┌────┬────┐    ┌────┬────┐    ┌────┬────┐    ┌────┬────┐
│ 14 │  ●─┼───→│ 30 │  ●─┼───→│ 25 │  ●─┼───→│ 42 │ NULL│
└────┴────┘    └────┴────┘    └────┴────┘    └────┴────┘
plain
Copy

The linked list is a collection of elements called **nodes**, each of which stores two items of information:
- An element of the list (data)
- A link (pointer to the next node)

The `NULL` in the last node indicates that it is the last node in the list.

---

## Arrays vs Linked Lists

### Limitations of Arrays:
- Arrays have a **fixed dimension** — once size is decided, it cannot be changed during execution
- **Insertion** is tedious — elements must be shifted one position to the right
- **Deletion** is inefficient — elements must be shifted one position to the left

### Advantages of Linked Lists:
- Can **grow and shrink** in size during its lifetime
- **No maximum size** limitation
- **No shifting** of elements required during insertion or deletion

---

## Operations on A Linked List

### Program 3-1: Implementation of various linked list operations

```c
#include <stdio.h>
#include <stdlib.h>

struct node
{
    int data;
    struct node *link;
};

void append(struct node **, int);
void addatbeg(struct node **, int);
void addafter(struct node *, int, int);
void display(struct node *);
int count(struct node *);
void del(struct node **, int);

int main()
{
    struct node *p;
    p = NULL; /* empty linked list */
    
    printf("No. of elements in the Linked List = %d\n", count(p));
    
    append(&p, 14);
    append(&p, 30);
    append(&p, 25);
    append(&p, 42);
    append(&p, 17);
    display(p);
    
    addatbeg(&p, 99);
    addatbeg(&p, 88);
    addatbeg(&p, 77);
    display(p);
    
    addafter(p, 3, 41);
    addafter(p, 6, 89);
    addafter(p, 10, 60);
    display(p);
    
    printf("No. of elements in the Linked List = %d\n", count(p));
    
    del(&p, 99);
    del(&p, 42);
    del(&p, 10);
    display(p);
    
    printf("No. of elements in the linked list = %d\n", count(p));
    return 0;
}
Function: append() — Add node at the end
c
Copy
void append(struct node **q, int num)
{
    struct node *temp, *r;
    
    if (*q == NULL) /* if the list is empty, create first node */
    {
        temp = (struct node *)malloc(sizeof(struct node));
        temp->data = num;
        temp->link = NULL;
        *q = temp;
    }
    else
    {
        temp = *q;
        /* go to last node */
        while (temp->link != NULL)
            temp = temp->link;
        
        /* add node at the end */
        r = (struct node *)malloc(sizeof(struct node));
        r->data = num;
        r->link = NULL;
        temp->link = r;
    }
}
Function: addatbeg() — Add node at the beginning
c
Copy
void addatbeg(struct node **q, int num)
{
    struct node *temp;
    
    /* add new node */
    temp = (struct node *)malloc(sizeof(struct node));
    temp->data = num;
    temp->link = *q;
    *q = temp;
}
Function: addafter() — Add node after specified position
c
Copy
void addafter(struct node *q, int loc, int num)
{
    struct node *temp, *r;
    int i;
    
    temp = q;
    /* skip to desired portion */
    for (i = 0; i < loc; i++)
    {
        temp = temp->link;
        /* if end of linked list is encountered */
        if (temp == NULL)
        {
            printf("There are less than %d elements in list\n", loc);
            return;
        }
    }
    
    /* insert new node */
    r = (struct node *)malloc(sizeof(struct node));
    r->data = num;
    r->link = temp->link;
    temp->link = r;
}
Function: display() — Display the linked list
c
Copy
void display(struct node *q)
{
    /* traverse the entire linked list */
    while (q != NULL)
    {
        printf("%d ", q->data);
        q = q->link;
    }
    printf("\n");
}
Function: count() — Count number of nodes
c
Copy
int count(struct node *q)
{
    int c = 0;
    /* traverse the entire linked list */
    while (q != NULL)
    {
        q = q->link;
        c++;
    }
    return c;
}
Function: del() — Delete a specified node
c
Copy
void del(struct node **q, int num)
{
    struct node *old, *temp;
    
    temp = *q;
    while (temp != NULL)
    {
        if (temp->data == num)
        {
            /* if node to be deleted is the first node */
            if (temp == *q)
                *q = temp->link;
            /* deletes the intermediate nodes */
            else
                old->link = temp->link;
            
            free(temp); /* free the memory occupied by the node */
            return;
        }
        else
        {
            old = temp;    /* old points to the previous node */
            temp = temp->link; /* go to the next node */
        }
    }
    printf("Element %d not found\n", num);
}
Output:
plain
Copy
No. of elements in the Linked List = 0
14 30 25 42 17
77 88 99 14 30 25 42 17
77 88 99 41 14 30 89 25 42 17 60
No. of elements in the Linked List = 11
Element 10 not found
77 88 41 14 30 89 25 17 60
No. of elements in the linked list = 9
More Linked Lists
A linked list can virtually be used for storing any similar data:
Table
Copy
Type	Example
Linked list of floats	2.53 → 8.44 → 4.67 → 3.90 → 6.12
Linked list of names	Ashok → Rajan → Vijay → Sanjay
Linked list of structures	(Ajay,24,5000) → (Rama,30,9000) → (Nimish,28,3000) → (Renu,25,7000)
Reversing the Links
Program 3-2: Program to reverse a linked list
c
Copy
void reverse(struct node **x)
{
    struct node *q, *r, *s;
    
    q = *x;
    r = NULL;
    
    /* traverse the entire linked list */
    while (q != NULL)
    {
        s = r;
        r = q;
        q = q->link;
        r->link = s;
    }
    *x = r;
}
Logic: Uses three pointers (q, r, s) to reverse links while traversing:
q — current node
r — previous node
s — stores previous of previous
Concatenation and Erasing
Program 3-3: Concatenate and erase linked lists
c
Copy
/* concatenates two linked lists */
void concat(struct node **p, struct node **q)
{
    struct node *temp;
    
    if (*p == NULL)
        *p = *q;
    else
    {
        if (*q != NULL)
        {
            temp = *p;
            /* traverse the entire first linked list */
            while (temp->link != NULL)
                temp = temp->link;
            temp->link = *q; /* concatenate the second list */
        }
    }
}

/* erases all the nodes from a linked list */
struct node *erase(struct node *q)
{
    struct node *temp;
    
    while (q != NULL)
    {
        temp = q;
        q = q->link;
        free(temp);
    }
    return NULL;
}
Recursive Operations on Linked List
Program 3-4: Recursive functions
c
Copy
/* counts the number of nodes in a linked list */
int length(struct node *q)
{
    static int l;
    if (q == NULL)
        return 0;
    else
    {
        l = 1 + length(q->link);
        return l;
    }
}

/* compares 2 linked lists. Returns 1 if equal, 0 otherwise */
int compare(struct node *q, struct node *r)
{
    static int flag;
    if ((q == NULL) && (r == NULL))
        flag = 1;
    else
    {
        if (q == NULL || r == NULL)
            flag = 0;
        if (q->data != r->data)
            flag = 0;
        else
            compare(q->link, r->link);
    }
    return flag;
}

/* copies a linked list into another */
void copy(struct node *q, struct node **s)
{
    if (q != NULL)
    {
        *s = (struct node *)malloc(sizeof(struct node));
        (*s)->data = q->data;
        (*s)->link = NULL;
        copy(q->link, &((*s)->link));
    }
}

/* adds a new node at the end of the linked list */
void addatend(struct node **s, int num)
{
    if (*s == NULL)
    {
        *s = (struct node *)malloc(sizeof(struct node));
        (*s)->data = num;
        (*s)->link = NULL;
    }
    else
        addatend(&((*s)->link), num);
}
Doubly Linked Lists
In a doubly linked list, each node stores:
Address of previous node
Data
Address of next node
Node Structure
Table
Copy
prev	data	next
Example
plain
Copy
NULL ←┬─[N|11|●]←→[●|2|●]←→[●|14|N]─┬→ NULL
      └──────────────────────────────┘
Program 3-5: Doubly Linked List Implementation
c
Copy
struct dnode
{
    struct dnode *prev;
    int data;
    struct dnode *next;
};
Function: d_append() — Add at end
c
Copy
void d_append(struct dnode **s, int num)
{
    struct dnode *r, *q = *s;
    
    if (*s == NULL) /* if the linked list is empty */
    {
        *s = (struct dnode *)malloc(sizeof(struct dnode));
        (*s)->prev = NULL;
        (*s)->data = num;
        (*s)->next = NULL;
    }
    else
    {
        while (q->next != NULL)
            q = q->next;
        
        r = (struct dnode *)malloc(sizeof(struct dnode));
        r->data = num;
        r->next = NULL;
        r->prev = q;
        q->next = r;
    }
}
Function: d_addatbeg() — Add at beginning
c
Copy
void d_addatbeg(struct dnode **s, int num)
{
    struct dnode *q;
    
    q = (struct dnode *)malloc(sizeof(struct dnode));
    q->prev = NULL;
    q->data = num;
    q->next = *s;
    (*s)->prev = q;
    *s = q;
}
Function: d_delete() — Delete a node
c
Copy
void d_delete(struct dnode **s, int num)
{
    struct dnode *q = *s;
    
    while (q != NULL)
    {
        if (q->data == num)
        {
            /* if node to be deleted is the first node */
            if (q == *s)
            {
                *s = (*s)->next;
                (*s)->prev = NULL;
            }
            else
            {
                /* if node to be deleted is the last node */
                if (q->next == NULL)
                    q->prev->next = NULL;
                else /* intermediate node */
                {
                    q->prev->next = q->next;
                    q->next->prev = q->prev;
                }
            }
            free(q);
            return;
        }
        q = q->next;
    }
    printf("%d not found.\n", num);
}
Chapter Summary
Table
Copy
Feature	Singly Linked List	Doubly Linked List
Pointers per node	1 (next)	2 (prev, next)
Memory	Less	More
Traversal	Forward only	Both directions
Previous node access	Not possible directly	Direct access
Implementation	Simpler	More complex
Key Points:
(a) Linked List is a linear data structure used to store similar data
(b) Unlike an array, theres no need to specify size ahead of time
(c) Linked list is implemented using structure data type
(d) Linked list may be singly linked or doubly linked
(e) Singly linked lists have a single pointer pointing to the next node
(f) Doubly linked lists have two pointers (prev and next)
Check Your Progress
True or False:
(a) Linked list is used to store similar data.
(b) All nodes in the linked may be in non-contiguous memory locations.
(c) The link part of the last node in a singly linked list always contains NULL.
(d) In a singly linked list, if we lose the location of the first node it is as good as having lost the entire linked list.
(e) Doubly linked list facilitates movement from one node to another in either direction.
(f) A doubly linked list will occupy less memory as compared to a corresponding singly linked list.
(g) If we are to traverse from first node to last node it would be faster to do so if the linked list is singly linked instead of doubly linked.
(h) In a structure used to represent the node of a doubly linked list it is necessary that the structure elements are in the order backward link, data, forward link.
Exercises
Level II
(a) Write a program that reads the name, age and salary of 10 persons and maintains them in a linked list sorted by name.
(b) Given two linked lists A and B, create:
Linked list C containing only common elements
Linked list D containing all elements (union, no repetition)
(c) Combine two lists A: 7,5,3,1,20 and B: 6,25,32,11,9 into: 7,6,5,25,3,32,1,11,20,9 without creating additional nodes.
Level III
(a) Split a linked list containing positive and negative numbers into two separate lists.
(b) Write a program to delete duplicate elements in a linked list.
Case Scenario: Polynomials using Linked List
Polynomials like 5x⁴ + 2x³ + 7x² + 10x - 8 can be maintained using a linked list where each node contains:
Coefficient
Exponent
Link to next term
Write a program to build a linked list to represent a polynomial and perform addition and multiplication operations.
