---
title: Stack as a Linked List
weight: 3
---

In the earlier section we had used arrays to store the elements that get added to the stack. However, when implemented as an array it suffers from the basic limitation of an array—that its size cannot be increased or decreased once it is declared. As a result, one ends up reserving either too much memory or too less memory for an array and in turn for a stack. This problem can be overcome if we implement a stack using a linked list.

Each node in the linked list contains the data and a pointer that gives location of the next node in the list. The pointer to the beginning of the list serves the purpose of the top of the stack. Figure 5-2 shows the linked list representation of a stack.

![Figure 5-2: Representation of stack as a linked list](image-placeholder)

Let us now see a program that implements stack as a linked list.

---

### Program 5-2: Stack as a linked list

```c
#include <stdio.h>
#include <stdlib.h>

struct node {
    int data;
    struct node *link;
};

void push(struct node **, int);
int pop(struct node **);
void delstack(struct node **);

int main() {
    struct node *s = NULL;
    int n;
    
    push(&s, 14);
    push(&s, -3);
    push(&s, 18);
    push(&s, 29);
    push(&s, 31);
    push(&s, 16);
    
    n = pop(&s);
    if (n != NULL)
        printf("Item popped: %d\n", n);
    
    n = pop(&s);
    if (n != NULL)
        printf("Item popped: %d\n", n);
    
    n = pop(&s);
    if (n != NULL)
        printf("Item popped: %d\n", n);
    
    delstack(&s);
    
    return 0;
}

/* adds a new node at beginning of linked list */
void push(struct node **top, int item) {
    struct node *temp;
    temp = (struct node *)malloc(sizeof(struct node));
    if (temp == NULL)
        printf("Stack is full\n");
    temp->data = item;
    temp->link = *top;
    *top = temp;
}

/* deletes a node from beginning of linked list */
int pop(struct node **top) {
    struct node *temp;
    int item;
    
    if (*top == NULL) {
        printf("Stack is empty\n");
        return NULL;
    }
    temp = *top;
    item = temp->data;
    *top = (*top)->link;
    free(temp);
    return item;
}

/* deallocates memory */
void delstack(struct node **top) {
    struct node *temp;
    
    if (*top == NULL)
        return;
    
    while (*top != NULL) {
        temp = *top;
        *top = (*top)->link;
        free(temp);
    }
}
```

### Output:
```
Item popped: 16
Item popped: 31
Item popped: 29
```

### Explanation

Here we have declared a structure called `node`. The variable `s` is a pointer to the structure `node`. Initially `s` is set to `NULL` to indicate that the stack is empty. In every call to the function `push()` we are creating a new node dynamically. As long as there is enough memory for dynamic allocation, `temp` would never become `NULL`. If value of `temp` happens to be `NULL` then that would be the stage when stack would become full.

After creating a new node, the pointer `s` should point to the newly created item of the list. Hence, we have assigned the address of this new node to `s` using the pointer `top`.

In the `pop()` function, first we are checking whether or not a stack is empty. If so, then a message 'Stack is empty' gets displayed. If the stack is not empty then the topmost item gets removed from the list.

---