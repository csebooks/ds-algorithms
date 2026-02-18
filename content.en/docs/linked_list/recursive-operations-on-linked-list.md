---
title: Recursive Operations on Linked List
weight: 7
---

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