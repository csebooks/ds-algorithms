---
title: A Few More Operations
weight: 6
---

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