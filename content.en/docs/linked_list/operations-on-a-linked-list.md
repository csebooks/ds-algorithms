---
title: Operations on A Linked List
weight: 3
---

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