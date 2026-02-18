---
title: Reversing the Links
weight: 5
---

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