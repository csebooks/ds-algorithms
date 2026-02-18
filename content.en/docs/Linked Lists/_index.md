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

## Stay connected

### Why This Chapter Matters?

United we stand, divided we fall! More united and connected we are, more is the flexibility and scalability. Same is true with linked lists. Linked lists are used at numerous places in Computer Science. The flexibility and performance they offer is worth the pain of learning.

---

For storing similar data in memory we can use either an array or a linked list. Arrays are simple to understand and elements of an array are easily accessible. But arrays suffer from the following limitations:

- Arrays have a fixed dimension. Once the size of an array is decided it cannot be increased or decreased during execution.
- Insertion of a new element in an array is tedious because during insertion each element after the specified position has to be shifted one position to the right.
- Deletion of an existing element in an array is inefficient because during deletion each element after the specified position has to be shifted one position to the left.

Linked list overcomes all these disadvantages. A linked list can grow and shrink in size during its lifetime. Thus, there is no maximum size of a linked list. Also, unlike arrays, while inserting or deleting elements in a linked list shifting of existing elements is not required.

---

## What is a Linked List?

While the elements of an array occupy contiguous memory locations, those of a linked list are not constrained to be stored in adjacent locations. The order of the elements is maintained by explicit links between them. For instance, the marks obtained by different students can be stored in a linked list as shown in Figure 3-1.

![Figure 3-1: Linked list](image-placeholder)

Observe that the linked list is a collection of elements called **nodes**, each of which stores two items of information—an element of the list and a link. In Figure 3-1, the data part of each node consists of the marks obtained by a student and the link part contains address of the next node. Thus, the link part is a pointer to the next node. Hence it is shown using an arrow. The NULL (N) in the last node indicates that it is the last node in the list.

---

## Operations on A Linked List

Several operations can be performed on linked lists. This includes building a linked list by adding new node (at the beginning, at the end or in the middle of the linked list), deleting a node, display contents of all nodes, etc. The following program shows how to implement these operations. Go through the program carefully, a step at a time to understand the working of these operations.

---

### Program 3-1: Implementation of various linked list operations

```c
#include <stdio.h>
#include <stdlib.h>

struct node {
    int data;
    struct node *link;
};

void append(struct node **, int);
void addatbeg(struct node **, int);
void addafter(struct node *, int, int);
void display(struct node *);
int count(struct node *);
void del(struct node **, int);

int main() {
    struct node *p;
    p = NULL;  /* empty linked list */
    
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

/* adds a node at the end of a linked list */
void append(struct node **q, int num) {
    struct node *temp, *r;
    
    if (*q == NULL) {  /* if the list is empty, create first node */
        temp = (struct node *)malloc(sizeof(struct node));
        temp->data = num;
        temp->link = NULL;
        *q = temp;
    }
    else {
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

/* adds a new node at the beginning of the linked list */
void addatbeg(struct node **q, int num) {
    struct node *temp;
    
    /* add new node */
    temp = (struct node *)malloc(sizeof(struct node));
    temp->data = num;
    temp->link = *q;
    *q = temp;
}

/* adds a new node after the specified number of nodes */
void addafter(struct node *q, int loc, int num) {
    struct node *temp, *r;
    int i;
    
    temp = q;
    /* skip to desired portion */
    for (i = 0; i < loc; i++) {
        temp = temp->link;
        /* if end of linked list is encountered */
        if (temp == NULL) {
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

/* displays the contents of the linked list */
void display(struct node *q) {
    /* traverse the entire linked list */
    while (q != NULL) {
        printf("%d ", q->data);
        q = q->link;
    }
    printf("\n");
}

/* counts the number of nodes present in the linked list */
int count(struct node *q) {
    int c = 0;
    /* traverse the entire linked list */
    while (q != NULL) {
        q = q->link;
        c++;
    }
    return c;
}

/* deletes the specified node from the linked list */
void del(struct node **q, int num) {
    struct node *old, *temp;
    
    temp = *q;
    while (temp != NULL) {
        if (temp->data == num) {
            /* if node to be deleted is the first node in the linked list */
            if (temp == *q)
                *q = temp->link;
            /* deletes the intermediate nodes in the linked list */
            else
                old->link = temp->link;
            
            free(temp);  /* free the memory occupied by the node */
            return;
        }
        /* traverse the linked list till the last node is reached */
        else {
            old = temp;  /* old points to the previous node */
            temp = temp->link;  /* go to the next node */
        }
    }
    printf("Element %d not found\n", num);
}
```

### Output:
```
No. of elements in the Linked List = 0
14 30 25 42 17
77 88 99 14 30 25 42 17
77 88 99 41 14 30 89 25 42 17 60
No. of elements in the Linked List = 11
Element 10 not found
77 88 41 14 30 89 25 17 60
No. of elements in the linked list = 9
```

### Explanation

To begin with we have defined a structure for a node. It contains a data part and a link part. The variable `p` has been declared as pointer to a node. We have used `p` as pointer to the first node in the linked list. No matter how many nodes get added to the linked list, `p` would continue to point to the first node in the list. When no node has been added to the list, `p` has been set to `NULL` to indicate that the list is empty.

#### The `append()` function

The `append()` function has to deal with two situations:
- (a) The node is being added to an empty list.
- (b) The node is being added at the end of an existing list.

In the first case, the condition `if (*q == NULL)` gets satisfied. Hence, firstly memory is allocated for the node using `malloc()`. Then data and the link part of this node are set up using the statements:
```c
temp->data = num;
temp->link = NULL;
```
Lastly, `p` is made to point to this node, since the first node has been added to the list and `p` must always point to the first node. Note that since `q` contains address of `p`, `*q` is nothing but equal to `p`.

In the other case, when the linked list is not empty, the condition `if (*q == NULL)` will fail, since `*q` (i.e. `p`) is non-NULL. Now `temp` is made to point to the first node in the list through the statement `temp = *q;`. Then using `temp` the entire linked list is traversed using the statements:
```c
while (temp->link != NULL)
    temp = temp->link;
```

The position of the pointers before and after traversing the linked list is shown in Figure 3-2.

![Figure 3-2: Working of append() function](image-placeholder)

Each time through the loop the statement `temp = temp->link` makes `temp` point to the next node in the list. When `temp` reaches the last node the condition `temp->link != NULL` will fail. Once outside the loop, we allocate memory for the new node through the statement:
```c
r = (struct node *)malloc(sizeof(struct node));
```
Then this new node's data part is set with `num` and link part with `NULL`. Note that this node is now going to be the last node in the list.

Now we need to connect the previous last node (pointed to by `temp`) with the new last node (pointed to by `r`). This is done through the statement:
```c
temp->link = r;
```

How does the statement `temp = temp->link` makes `temp` point to the next node in the list? Let us understand this with the help of an example. Suppose in a linked list containing 4 nodes, `temp` is pointing to the first node. This linked list is shown in Figure 3-3.

![Figure 3-3: Connection of nodes](image-placeholder)

Instead of showing the links to the next node we have shown the addresses of the next node in the link part of each node.

When we execute the statement `temp = temp->link;` the right-hand side yields 100. This address is now stored in `temp`. As a result, `temp` starts pointing to the node present at address 100. In effect, the statement has shifted `temp` so that it has started pointing to the next node in the list.

#### The `addatbeg()` function

Let us now understand the `addatbeg()` function. Suppose there are already 5 nodes in the list and we wish to add a new node at the beginning of this existing linked list. This situation is shown in Figure 3-4.

![Figure 3-4: Working of addatbeg()](image-placeholder)

For adding a new node at the beginning, firstly memory is allocated for this node and data is stored in it through the statement `temp->data = num;`.

Now we need to make the link part of this node point to the existing first node. This has been achieved through the statement:
```c
temp->link = *q;
```
Lastly, this new node must be made the first node in the list. This has been attained through the statement:
```c
*q = temp;
```

#### The `addafter()` function

The `addafter()` function permits us to add a new node after a specified number of node in the linked list.

To begin with, through a loop we skip the desired number of nodes after which a new node is to be added. Suppose we wish to add a new node containing data as 41 after the 3rd node in the list. The position of pointers once the control reaches outside the for loop is shown in Figure 3-5(a). Now memory is allocated for the node to be inserted and 41 is stored in the data part of it.

![Figure 3-5: Working of addafter() function](image-placeholder)

All that remains to be done is readjustment of links such that 41 goes in between 77 and 14. This is achieved through the statements:
```c
r->link = temp->link;
temp->link = r;
```
The first statement makes link part of node containing 41 to point to the node containing 14. The second statement ensures that the link part of node containing 77 points to the node containing 41. On execution of the second statement the earlier link between 77 and 14 is severed. So now 77 no longer points to 14, it points to 41.

The `display()` and `count()` functions are straight forward.

#### The `del()` function

That brings us to the last function in the program, i.e., `del()`. In this function through the while loop, we have traversed through the entire linked list, checking at each node, whether it is the node to be deleted. If so, we have checked if the node being deleted is the first node in the linked list. If it is so, we have simply shifted `p` (which is same as `*q`) to the next node and then deleted the earlier node.

If the node to be deleted is an intermediate node, then the position of various pointers and links before and after the deletion is shown in Figure 3-6.

![Figure 3-6: Working of del() function](image-placeholder)

---

## More Linked Lists

A common and a wrong impression that beginners carry is that a linked list is used only for storing integers. However, a linked list can virtually be used for storing any similar data. For example, there can be a linked list of floats, a linked list of names, or even a linked list of records, where each record contains name, age and salary of an employee. These linked lists are shown in Figure 3-7.

![Figure 3-7: Different types of linked list](image-placeholder)

---

## Reversing the Links

Having had a feel of linked list, let us now explore some more operations that can be performed on a linked list. How about reversing the links in the existing linked list such that the last node becomes the first node and the first becomes the last? Here is a program that shows how this reversal of links can be achieved.

---

### Program 3-2: Program to reverse a linked list

```c
#include <stdio.h>
#include <stdlib.h>

struct node {
    int data;
    struct node *link;
};

void addatbeg(struct node **, int);
void reverse(struct node **);
void display(struct node *);
int count(struct node *);

int main() {
    struct node *p;
    p = NULL;  /* empty linked list */
    
    addatbeg(&p, 7);
    addatbeg(&p, 43);
    addatbeg(&p, 17);
    addatbeg(&p, 3);
    addatbeg(&p, 23);
    addatbeg(&p, 5);
    
    display(p);
    reverse(&p);
    display(p);
    
    return 0;
}

/* adds a new node at the beginning of the linked list */
void addatbeg(struct node **q, int num) {
    struct node *temp;
    
    /* add new node */
    temp = (struct node *)malloc(sizeof(struct node));
    temp->data = num;
    temp->link = *q;
    *q = temp;
}

void reverse(struct node **x) {
    struct node *q, *r, *s;
    
    q = *x;
    r = NULL;
    
    /* traverse the entire linked list */
    while (q != NULL) {
        s = r;
        r = q;
        q = q->link;
        r->link = s;
    }
    *x = r;
}

/* displays the contents of the linked list */
void display(struct node *q) {
    /* traverse the entire linked list */
    while (q != NULL) {
        printf("%d ", q->data);
        q = q->link;
    }
    printf("\n");
}
```

### Output:
```
5 23 3 17 43 7
7 43 17 3 23 5
```

### Explanation

The function `reverse()` receives the parameter `struct node **x` which is the address of the pointer to the first node of the linked list. To traverse the linked list a variable `q` of the type `struct node *` is required. We have initialized `q` with the value of `*x`. So, `q` also starts pointing to the first node.

To begin with, we need to store the NULL value in the link part of the first node, which is done through the statements:
```c
s = r;
r = q;
r->link = s;
```
`r` which is of the type `struct node *` is initialized to a NULL value. Since `r` contains NULL, `s` would also contain NULL. Now `r` is assigned `q` so that `r` also starts pointing to the first node. Finally, `r->link` is assigned `s` so that `r->link` becomes NULL, which is nothing but the link part of the first node.

But if we store a NULL value in the link part of the first node then the address of the second node will be lost. Hence, before storing a NULL value in the link part of the first node, `q` is made to point to the second node through the statement `q = q->link;`.

During the second iteration of the while loop, `r` points to the first node and `q` points to the second node. Now the link part of the second node should point to the first node. This is done through the same statements:
```c
s = r;
r = q;
r->link = s;
```
Since `r` points to the first node, `s` would also point to the first node. Now `r` is assigned the value of `q` so that `r` now starts pointing to the second node. Finally, `r->link` is assigned with `s` so that `r->link` starts pointing to the first node. But if we store the value of `s` in the link part of second node, then the address of the third node would be lost. Hence, before storing the value of `s` in `r->link`, `q` is made to point to the third node through the statement `q = q->link;`.

While traversing the nodes through the while loop each time `q` starts pointing to the next node in the list and `r` starts pointing to the previous node. As a result, when the while loop ends all the links have been adjusted properly such that last node becomes the first node and first node becomes the last node.

Finally, once outside the while loop, the statement `*x = r` is executed. This ensures that the pointer `p` now starts pointing to the node, which is the last node of the original list. This is shown in Figure 3-8.

![Figure 3-8: Reversing the links](image-placeholder)

---

## A Few More Operations

If you think carefully, you can list out so many operations that can be performed on a linked list. For example, concatenating one linked list at the end of another, deleting all nodes present in a linked list, modifying certain elements in a linked list, etc. Given below is a program for concatenation of linked list and erasing all nodes in the list.

---

### Program 3-3: Program to concatenate and erase a linked list

```c
#include <stdio.h>
#include <stdlib.h>

struct node {
    int data;
    struct node *link;
};

void append(struct node **, int);
void concat(struct node **, struct node **);
void display(struct node *);
int count(struct node *);
struct node *erase(struct node *);

int main() {
    struct node *first, *second;
    first = second = NULL;  /* empty linked lists */
    
    append(&first, 1);
    append(&first, 2);
    append(&first, 3);
    append(&first, 4);
    printf("First List:\n");
    display(first);
    printf("No. of ele. in first Linked List = %d\n", count(first));
    
    append(&second, 5);
    append(&second, 6);
    append(&second, 7);
    append(&second, 8);
    printf("Second List:\n");
    display(second);
    printf("No. of ele. in second Linked List = %d\n", count(second));
    
    /* the result obtained after concatenation is in the first list */
    concat(&first, &second);
    printf("Concatenated List:\n");
    display(first);
    printf("No. of elements before erasing = %d\n", count(first));
    
    first = erase(first);
    printf("No. of elements after erasing = %d\n", count(first));
    
    return 0;
}

/* adds a node at the end of a linked list */
void append(struct node **q, int num) {
    struct node *temp;
    temp = *q;
    
    if (*q == NULL) {  /* if the list is empty, create first node */
        *q = (struct node *)malloc(sizeof(struct node));
        temp = *q;
    }
    else {
        /* go to last node */
        while (temp->link != NULL)
            temp = temp->link;
        
        /* add node at the end */
        temp->link = (struct node *)malloc(sizeof(struct node));
        temp = temp->link;
    }
    
    /* assign data to the last node */
    temp->data = num;
    temp->link = NULL;
}

/* concatenates two linked lists */
void concat(struct node **p, struct node **q) {
    struct node *temp;
    
    /* if the first linked list is empty */
    if (*p == NULL)
        *p = *q;
    else {
        /* if both linked lists are non-empty */
        if (*q != NULL) {
            temp = *p;  /* points to the starting of the first list */
            
            /* traverse the entire first linked list */
            while (temp->link != NULL)
                temp = temp->link;
            
            temp->link = *q;  /* concatenate the second list after the first */
        }
    }
}

/* displays the contents of the linked list */
void display(struct node *q) {
    /* traverse the entire linked list */
    while (q != NULL) {
        printf("%d ", q->data);
        q = q->link;
    }
    printf("\n");
}

/* counts the number of nodes present in the linked list */
int count(struct node *q) {
    int c = 0;
    /* traverse the entire linked list */
    while (q != NULL) {
        q = q->link;
        c++;
    }
    return c;
}

/* erases all the nodes from a linked list */
struct node *erase(struct node *q) {
    struct node *temp;
    
    /* traverse till the end erasing each node */
    while (q != NULL) {
        temp = q;
        q = q->link;
        free(temp);  /* free the memory occupied by the node */
    }
    return NULL;
}
```

### Output:
```
First List:
1 2 3 4
No. of elements in the first Linked List = 4
Second List:
5 6 7 8
No. of elements in the second Linked List = 4
Concatenated List:
1 2 3 4 5 6 7 8
No. of elements in Linked List before erasing = 8
No. of elements in Linked List after erasing = 0
```

---

## Recursive Operations on Linked List

In C, it is possible for the functions to call themselves. A function is called 'recursive' if a statement within the body of a function calls the same function. Some of the operations that are carried out on linked lists can be easily implemented using recursion. These include counting the number of nodes present in a linked list, comparing two linked lists, copying one linked list into another, adding a new node at the end of the linked list, etc.

Given below are the functions for carrying out each of these operations. These functions are pretty straight-forward. Hence, I would omit the discussion about working of each of them. You can call these functions from `main()` after creating suitable linked lists using the `addatend()` function discussed in earlier section.

---

### Program 3-4: Recursive functions to count nodes in a linked list, comparing two linked lists, cloning a linked list and adding a new node at the end of a linked list

```c
/* counts the number of nodes in a linked list */
int length(struct node *q) {
    static int l;
    
    /* if list is empty or if NULL is encountered */
    if (q == NULL)
        return (0);
    else {
        l = 1 + length(q->link);
        return (l);
    }
}

/* compares 2 linked lists. Returns 1 if they are equal, 0 otherwise */
int compare(struct node *q, struct node *r) {
    static int flag;
    
    if ((q == NULL) && (r == NULL))
        flag = 1;
    else {
        if (q == NULL || r == NULL)
            flag = 0;
        if (q->data != r->data)
            flag = 0;
        else
            compare(q->link, r->link);
    }
    return (flag);
}

/* copies a linked list into another */
void copy(struct node *q, struct node **s) {
    if (q != NULL) {
        *s = (struct node *)malloc(sizeof(struct node));
        (*s)->data = q->data;
        (*s)->link = NULL;
        copy(q->link, &((*s)->link));
    }
}

/* adds a new node at the end of the linked list */
void addatend(struct node **s, int num) {
    if (*s == NULL) {
        *s = (struct node *)malloc(sizeof(struct node));
        (*s)->data = num;
        (*s)->link = NULL;
    }
    else
        addatend(&((*s)->link), num);
}
```

---

## Doubly Linked Lists

In the linked lists that we have used so far, each node provides information about where is the next node in the list. It has no knowledge about where the previous node lies in memory. If we are at say the 15th node in the list, then to reach the 14th node we have to traverse the list right from the first node. To avoid this, we can store in each node not only the address of next node but also the address of the previous node in the linked list. This arrangement is often known as a **'Doubly Linked List'** and is shown in Figure 3-9.

![Figure 3-9: Doubly linked list](image-placeholder)

The following program implements the Doubly Linked List (DLL).

---

### Program 3-4: Program to implement a doubly linked list

```c
#include <stdio.h>
#include <stdlib.h>

/* structure representing a node of the doubly linked list */
struct dnode {
    struct dnode *prev;
    int data;
    struct dnode *next;
};

void d_append(struct dnode **, int);
void d_addatbeg(struct dnode **, int);
void d_addafter(struct dnode *, int, int);
void d_display(struct dnode *);
int d_count(struct dnode *);
void d_delete(struct dnode **, int);

int main() {
    struct dnode *p;
    p = NULL;  /* empty doubly linked list */
    
    d_append(&p, 11);
    d_append(&p, 2);
    d_append(&p, 14);
    d_append(&p, 17);
    d_append(&p, 99);
    d_display(p);
    printf("No. of elements in the DLL = %d\n", d_count(p));
    
    d_addatbeg(&p, 33);
    d_addatbeg(&p, 55);
    d_display(p);
    printf("No. of elements in the DLL = %d\n", d_count(p));
    
    d_addafter(p, 4, 66);
    d_addafter(p, 2, 96);
    d_display(p);
    printf("No. of elements in the DLL = %d\n", d_count(p));
    
    d_delete(&p, 55);
    d_delete(&p, 2);
    d_delete(&p, 99);
    d_display(p);
    printf("No. of elements in the DLL = %d\n", d_count(p));
    
    return 0;
}

/* adds a new node at the end of the doubly linked list */
void d_append(struct dnode **s, int num) {
    struct dnode *r, *q = *s;
    
    /* if the linked list is empty */
    if (*s == NULL) {
        /* create a new node */
        *s = (struct dnode *)malloc(sizeof(struct dnode));
        (*s)->prev = NULL;
        (*s)->data = num;
        (*s)->next = NULL;
    }
    else {
        /* traverse the linked list till the last node is reached */
        while (q->next != NULL)
            q = q->next;
        
        /* add a new node at the end */
        r = (struct dnode *)malloc(sizeof(struct dnode));
        r->data = num;
        r->next = NULL;
        r->prev = q;
        q->next = r;
    }
}

/* adds a new node at the beginning of the linked list */
void d_addatbeg(struct dnode **s, int num) {
    struct dnode *q;
    
    /* create a new node */
    q = (struct dnode *)malloc(sizeof(struct dnode));
    
    /* assign data and pointer to the new node */
    q->prev = NULL;
    q->data = num;
    q->next = *s;
    
    /* make new node the head node */
    (*s)->prev = q;
    *s = q;
}

/* adds a new node after the specified number of nodes */
void d_addafter(struct dnode *q, int loc, int num) {
    struct dnode *temp;
    int i;
    
    /* skip to desired portion */
    for (i = 0; i < loc; i++) {
        q = q->next;
        /* if end of linked list is encountered */
        if (q == NULL) {
            printf("There are less than %d elements\n", loc);
            return;
        }
    }
    
    /* insert new node */
    q = q->prev;
    temp = (struct dnode *)malloc(sizeof(struct dnode));
    temp->data = num;
    temp->prev = q;
    temp->next = q->next;
    temp->next->prev = temp;
    q->next = temp;
}

/* displays the contents of the linked list */
void d_display(struct dnode *q) {
    /* traverse the entire linked list */
    while (q != NULL) {
        printf("%2d\t", q->data);
        q = q->next;
    }
    printf("\n");
}

/* counts the number of nodes present in the linked list */
int d_count(struct dnode *q) {
    int c = 0;
    /* traverse the entire linked list */
    while (q != NULL) {
        q = q->next;
        c++;
    }
    return c;
}

/* deletes the specified node from the doubly linked list */
void d_delete(struct dnode **s, int num) {
    struct dnode *q = *s;
    
    /* traverse the entire linked list */
    while (q != NULL) {
        /* if node to be deleted is found */
        if (q->data == num) {
            /* if node to be deleted is the first node */
            if (q == *s) {
                *s = (*s)->next;
                (*s)->prev = NULL;
            }
            else {
                /* if node to be deleted is the last node */
                if (q->next == NULL)
                    q->prev->next = NULL;
                else
                /* if node to be deleted is any intermediate node */
                {
                    q->prev->next = q->next;
                    q->next->prev = q->prev;
                }
            }
            free(q);
            return;  /* return back after deletion */
        }
        q = q->next;  /* go to next node */
    }
    printf("%d not found.\n", num);
}
```

### Output:
```
11  2  14  17  99
No. of elements in the DLL = 5
55  33  11  2  14  17  99
No. of elements in the DLL = 7
55  33  11  2  96  14  66  17  99
No. of elements in the DLL = 9
33  96  11  66  14  17
No. of elements in the DLL = 6
```

### Explanation

Let us now understand the different functions that we have defined in the program.

#### Function `d_append()`

The `d_append()` function adds a node at the end of the existing list. It also checks the special case of adding the first node if the list is empty.

This function accepts two parameters. The first parameter `s` is of type `struct dnode**` which contains the address of the pointer to the first node of the list or a NULL value in case of empty list. The second parameter `num` is an integer, which is to be added in the list.

To begin with we initialize `q` which is of the type `struct dnode *` with the value stored at `s`. This is done because using `q` the entire list is traversed if it is non-empty.

If the list is empty then the condition `if (*s == NULL)` gets satisfied. Now memory is allocated for the new node whose address is stored in `*s` (i.e. `p`). Using `s` a NULL value is stored in its `prev` and `next` links and the value of `num` is assigned to its data part.

If the list is non-empty then through the statements:
```c
while (q->next != NULL)
    q = q->next;
```
`q` is made to point to the last node of the list. Then memory is allocated for the node whose address is stored in `r`. A NULL value is stored in the `next` part of this node, because this is going to be last node. Now what remains to be done is to link this node with rest of the list. This is done through the statements:
```c
r->prev = q;
q->next = r;
```
The statement `r->prev = q` makes the `prev` part of the new node `r` to point to the previous node `q`. The statement `q->next = r` makes the `next` part of `q` to point to the last node `r`. This is shown in Figure 3-10.

![Figure 3-10: Addition of a node to a Doubly linked list](image-placeholder)

#### Function `d_addatbeg()`

The `d_addatbeg()` function adds a node at the beginning of the existing list. This function accepts two parameters. The first parameter `s` is of type `struct dnode**` which contains the address of the pointer to the first node and the second parameter `num` is an integer, which is to be added in the list.

Memory is allocated for the new node whose address is stored in `q`. Then `num` is stored in the data part of the new node. A NULL value is stored in `prev` part of the new node as this is going to be the first node of the list. The `next` part of this new node should contain the address of the first node of the list. This is done through the statement:
```c
q->next = *s;
```
Now what remains to be done is to store the address of this new node into the `prev` part of the first node and make this new node the first node in the list. This is done through the statements:
```c
(*s)->prev = q;
*s = q;
```
These operations are shown in Figure 3-11.

![Figure 3-11: Working of d_addatbeg() and d_addafter()](image-placeholder)

#### Function `d_addafter()`

The `d_addafter()` function adds a node at the specified position of an existing list. This operation of adding a new node in between two existing nodes can be better understood with the help of Figure 3-11.

This function accepts three parameters. The first parameter `q` points to the first node of the list. The second parameter `loc` specifies the node number after which the new node must be inserted. The third parameter `num` is an integer, which is to be added to the list.

A loop is executed to reach the position where the node is to be added. This loop also checks whether the position `loc` that we have mentioned, really occurs in the list or not. When the loop ends, we reach the `loc` position where the node is to be inserted. By this time `q` is pointing to the node before which the new node is to be added.

The statement `q = q->prev;` makes `q` to point to the node after which the new node should be added. Then memory is allocated for the new node and its address is stored in `temp`. The value of `num` is stored in the data part of the new node.

The `prev` part of the new node should point to `q`. This is done through the statement `temp->prev = q;`.

The `next` part of the new node should point to the node whose address is stored in the `next` part of node pointed to by `q`. This is achieved through the statement `temp->next = q->next;`.

Now what remains to be done is to make `prev` part of the next node (node pointed by `q->next`) to point to the new node. This is done through the statement `temp->next->prev = temp;`.

At the end, we change the `next` part of `q` to make it point to the new node, and this is done through the statement `q->next = temp;`.

#### Function `d_delete()`

The function `d_delete()` deletes a node from the list if the data part of that node matches `num`. This function receives two parameters. The first parameter is the address of the pointer to the first node and the second parameter is the number that is to be deleted.

We run a loop to traverse the list. Inside the loop the data part of each node is compared with the `num` value. If the `num` value matches the data part in the node then we need to check the position of the node to be deleted.

If it happens to be the first node, then the first node is made to point to the `next` part of the first node. This is done through the statement:
```c
*s = (*s)->next;
```
Then, a value NULL is stored in `prev` part of the second node, since it is now going to become the first node. This is done through the statement:
```c
(*s)->prev = NULL;
```

If the node to be deleted happens to be the last node, then NULL is stored in the `next` part of the second last node. This is done through the statements:
```c
if (q->next == NULL)
    q->prev->next = NULL;
```

If the node to be deleted happens to be any intermediate node, then the address of the next node is stored in the `next` part of the previous node and the address of the previous node is stored in the `prev` part of the next node. This is done through the statements:
```c
q->prev->next = q->next;
q->next->prev = q->prev;
```

Finally the memory occupied by the node being deleted is released by calling the function `free()`. Figure 3-12 shows the working of the `d_delete()` function.

![Figure 3-12: Working of d_delete()](image-placeholder)

---

# Chapter Bullets: Summary of chapter

- (a) Linked List is a linear data structure used to store similar data.
- (b) Unlike an array, in a linked list there's no need to specify how many elements you're going to store ahead of time. One can keep adding elements as long as there's enough memory in the machine.
- (c) Linked list is implemented using structure data type.
- (d) Linked list may be singly linked or doubly linked.
- (e) Singly linked lists have a single pointer pointing to the next node in the list. The last pointer is empty or points to null, signaling the end of the list.
- (f) Doubly linked lists have two pointers, one pointing to the next node and one pointing to the previous node. The first node's previous pointer points to null and the last node's next pointer points to null to signal the end of the list.

---

# Check Your Progress

## Exercise - Level I

### [A] State whether the following statements are True or False:

(a) Linked list is used to store similar data.

(b) All nodes in the linked may be in non-contiguous memory locations.

(c) The link part of the last node in a singly linked list always contains NULL.

(d) In a singly linked list, if we lose the location of the first node it is as good as having lost the entire linked list.

(e) Doubly linked list facilitates movement from one node to another in either direction.

(f) A doubly linked list will occupy less memory as compared to a corresponding singly linked list.

(g) If we are to traverse from first node to last node it would be faster to do so if the linked list is singly linked instead of doubly linked.

(h) In a structure used to represent the node of a doubly linked list it is necessary that the structure elements are in the order backward link, data, forward link.

---

## Sharpen Your Skills: Exercise - Level II

### [B] Answer the Following:

(a) Write a program that reads the name, age and salary of 10 persons and maintains them in a linked list sorted by name.

(b) There are two linked lists A and B containing the following data:
   - A: 3, 7, 10, 15, 16, 9, 22, 17, 32
   - B: 16, 2, 9, 13, 37, 8, 10, 1, 28

   Write a program to create:
   - A linked list C that contains only those elements that are common in linked list A and B.
   - A linked list D which contains all elements of A as well as B ensuring that there is no repetition of elements.

(c) There are two linked lists A and B containing the following data:
   - A: 7, 5, 3, 1, 20
   - B: 6, 25, 32, 11, 9

   Write a function to combine the two lists such that the resulting list contains nodes in the following elements:
   
   7, 6, 5, 25, 3, 32, 1, 11, 20, 9
   
   You are not allowed to create any additional node while writing the function.

---

## Coding Interview Questions: Exercise Level III

(a) A linked list contains some positive numbers and some negative numbers. Using this linked list write a program to create two new linked lists, one containing all positive numbers and the other containing all negative numbers.

(b) Write a program to delete duplicate elements in a linked list.

---

## Case Scenario Exercise: Polynomials using Linked List

Polynomials like 5x⁴ + 2x³ + 7x² + 10x - 8 can be maintained using a linked list. To achieve this each node should consist of three elements, namely coefficient, exponent and a link to the next term. Assume that the exponent of each successive term is less than that of the previous term. Write a program to build a linked list to represent a polynomial and perform common polynomial operations like addition and multiplication.
```