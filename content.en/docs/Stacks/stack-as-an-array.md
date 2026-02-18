---
title: Stack as an Array
weight: 2
---

Stack contains an ordered collection of elements. An array is used to store ordered list of elements. Hence, a stack can be implemented using an array. However, we are required to declare the size of the array before using it. So, when we use it to store elements of a stack the stack can grow or shrink within the memory reserved for the array. Let us now see a program that implements a stack using an array.

---

### Program 5-1: Stack as an array

```c
#include <stdio.h>

#define MAX 10

struct stack {
    int arr[MAX];
    int top;
};

void initstack(struct stack *);
void push(struct stack *, int item);
int pop(struct stack *);

int main() {
    struct stack s;
    int n;
    
    initstack(&s);
    
    push(&s, 2);
    push(&s, -4);
    push(&s, 8);
    push(&s, 11);
    
    n = pop(&s);
    if (n != NULL)
        printf("Item popped: %d\n", n);
    
    n = pop(&s);
    if (n != NULL)
        printf("Item popped: %d\n", n);
    
    n = pop(&s);
    if (n != NULL)
        printf("Item popped: %d\n", n);
    
    n = pop(&s);
    if (n != NULL)
        printf("Item popped: %d\n", n);
    
    n = pop(&s);
    if (n != NULL)
        printf("Item popped: %d\n", n);
    
    return 0;
}

/* initializes the stack */
void initstack(struct stack *s) {
    s->top = -1;
}

/* adds an element to the stack */
void push(struct stack *s, int item) {
    if (s->top == MAX - 1) {
        printf("Stack is full\n");
        return;
    }
    s->top++;
    s->arr[s->top] = item;
}

/* removes an element from the stack */
int pop(struct stack *s) {
    int data;
    if (s->top == -1) {
        printf("Stack is empty\n");
        return NULL;
    }
    data = s->arr[s->top];
    s->top--;
    return data;
}
```

### Output:
```
Item popped: 11
Item popped: 8
Item popped: -4
Item popped: 2
Stack is empty
```

### Explanation

In this program we have defined a structure called `stack`. The `push()` and `pop()` functions are respectively used to add and delete items from the top of the stack. The actual storage of stack elements is done in an array `arr`. The variable `top` is an index into this array. It contains a value where the addition or deletion is going to take place in the array, and thereby in the stack. To indicate that the stack is empty to begin with, the variable `top` is set with a value -1 by calling the function `initstack()`.

Every time an element is added to stack, it is verified whether such an addition is possible at all. If it is not, then the message 'Stack is full' is displayed. Since we have declared the array to hold 10 elements, the stack would be considered full if the value of top becomes equal to 9.

In `main()` we have called `push()` function to add 4 elements to the stack. Then we have removed these elements from the stack by calling the `pop()` function. When we call `pop()` for the 5th time, there are no elements present in the stack and `top` has a value -1 in it. Hence the 'Stack is empty' gets displayed.

---