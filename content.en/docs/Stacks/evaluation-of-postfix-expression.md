---
title: Evaluation of Postfix Expression
weight: 8
---

The virtue of postfix notation is that it enables easy evaluation of expressions. To begin with, the need for parentheses is eliminated. Secondly, the priority of the operators is no longer relevant. The expression can be evaluated by making a left to right scan, stacking operands, and evaluating operators using operands popped from the stack and finally placing the result onto the stack. This evaluation is much simpler than attempting a direct evaluation of infix notation. Let us now see a program to evaluate a postfix expression.

---

### Program 5-5: Evaluation of Postfix expression

```c
#include <stdio.h>
#include <stdlib.h>
#include <math.h>
#include <ctype.h>

#define MAX 50

struct postfix {
    int stack[MAX];
    int top, nn;
    char *s;
};

void initpostfix(struct postfix *);
void setexpr(struct postfix *, char *);
void push(struct postfix *, int);
int pop(struct postfix *);
void calculate(struct postfix *);
void show(struct postfix);

int main() {
    struct postfix q;
    char expr[MAX];
    
    initpostfix(&q);
    printf("Enter postfix expression to be evaluated:\n");
    gets(expr);
    setexpr(&q, expr);
    calculate(&q);
    show(q);
    
    return 0;
}

/* initializes structure elements */
void initpostfix(struct postfix *p) {
    p->top = -1;
}

/* sets s to point to the given expr. */
void setexpr(struct postfix *p, char *str) {
    p->s = str;
}

/* adds digit to the stack */
void push(struct postfix *p, int item) {
    if (p->top == MAX - 1)
        printf("Stack is full\n");
    else {
        p->top++;
        p->stack[p->top] = item;
    }
}

/* pops digit from the stack */
int pop(struct postfix *p) {
    int data;
    if (p->top == -1) {
        printf("Stack is empty\n");
        return NULL;
    }
    data = p->stack[p->top];
    p->top--;
    return data;
}

/* evaluates the postfix expression */
void calculate(struct postfix *p) {
    int n1, n2, n3;
    
    while (*(p->s)) {
        /* skip whitespace, if any */
        if (*(p->s) == ' ' || *(p->s) == '\t') {
            p->s++;
            continue;
        }
        
        /* if digit is encountered */
        if (isdigit(*(p->s))) {
            p->nn = *(p->s) - '0';
            push(p, p->nn);
        }
        else {
            /* if operator is encountered */
            n1 = pop(p);
            n2 = pop(p);
            
            switch (*(p->s)) {
                case '+':
                    n3 = n2 + n1;
                    break;
                case '-':
                    n3 = n2 - n1;
                    break;
                case '/':
                    n3 = n2 / n1;
                    break;
                case '*':
                    n3 = n2 * n1;
                    break;
                case '%':
                    n3 = n2 % n1;
                    break;
                case '$':
                    n3 = (int)pow((double)n2, (double)n1);
                    break;
                default:
                    printf("Unknown operator\n");
                    exit(1);
            }
            push(p, n3);
        }
        p->s++;
    }
}

/* displays the result */
void show(struct postfix p) {
    p.nn = pop(&p);
    printf("Result is: %d\n", p.nn);
}
```

### Output:
```
Enter postfix expression to be evaluated:
42$3*3-84/11+/+
Result is: 46
```

### Explanation

In this program the structure `postfix` contains an integer array `stack`, to store the intermediate results of the operations and `top` to store the position of the topmost element in the stack. The evaluation of the expression gets performed in the `calculate()` function.

During execution the user enters an arithmetic expression in postfix form. In the `calculate()` function, this expression gets scanned character by character. If the character scanned is a blank space, then it is skipped. If the character scanned is an operand, then first it is converted to a digit form (from string form), and then it is pushed onto the stack. If the character scanned is an operator, then the top two elements from the stack are popped, an arithmetic operation is performed between them and the result is then pushed back onto the stack. These steps are repeated as long as the string `s` is not exhausted. The `show()` function displays the final result. These steps can be better understood if you go through the evaluation of a sample postfix expression shown in Table 5-3.

### Table 5-3: Evaluation of Postfix

| Char. Scanned | Stack Contents |
|---------------|----------------|
| 4 | 4 |
| 2 | 4, 2 |
| $ | 16 |
| 3 | 16, 3 |
| * | 48 |
| 3 | 48, 3 |
| - | 45 |
| 8 | 45, 8 |
| 4 | 45, 8, 4 |
| / | 45, 2 |
| 1 | 45, 2, 1 |
| 1 | 45, 2, 1, 1 |
| + | 45, 2, 2 |
| / | 45, 1 |
| + | 46 (Result) |

---

# Chapter Bullets: Summary of chapter

- (a) Stack data structure is a LIFO list in which addition of new elements and deletion of existing elements takes place at the same end.
- (b) Addition of a new element to a stack is called **push** operation.
- (c) Deletion of an existing element from a stack is called **pop** operation.
- (d) Stack data structure can be implemented using an array or a linked list.
- (e) If stack is implemented as a linked list, push operation is like adding a new node at the beginning of the linked list.
- (f) If stack is implemented as a linked list, pop operation is like deleting an existing node from the beginning of the linked list.
- (g) Stack data structure has many applications like keeping track of function calls, storing local variable, evaluation of arithmetic expression, etc.

---

# Check Your Progress