---
title: Doubly Linked Lists
weight: 8
---

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