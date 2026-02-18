---
title: Infix to Postfix Conversion
weight: 5
---

Let us now see a program that converts an arithmetic expression given in an infix form to a postfix form.

---

### Program 5-3: Infix to Postfix conversion

```c
#include <stdio.h>
#include <string.h>
#include <ctype.h>

#define MAX 50

struct infix {
    char target[MAX];
    char stack[MAX];
    char *s, *t;
    int top;
};

void initinfix(struct infix *);
void setexpr(struct infix *, char *);
void push(struct infix *, char);
char pop(struct infix *);
void convert(struct infix *);
int priority(char);
void show(struct infix);

int main() {
    struct infix p;
    char expr[MAX];
    
    initinfix(&p);
    printf("Enter an expression in infix form:\n");
    gets(expr);
    setexpr(&p, expr);
    convert(&p);
    printf("The postfix expression is:\n");
    show(p);
    
    return 0;
}

/* initializes structure elements */
void initinfix(struct infix *p) {
    p->top = -1;
    strcpy(p->target, "");
    strcpy(p->stack, "");
    p->t = p->target;
    p->s = "";
}

/* sets s to point to given expression */
void setexpr(struct infix *p, char *str) {
    p->s = str;
}

/* adds an operator to the stack */
void push(struct infix *p, char c) {
    if (p->top == MAX)
        printf("Stack is full\n");
    else {
        p->top++;
        p->stack[p->top] = c;
    }
}

/* pops an operator from the stack */
char pop(struct infix *p) {
    if (p->top == -1) {
        printf("Stack is empty\n");
        return -1;
    }
    else {
        char item = p->stack[p->top];
        p->top--;
        return item;
    }
}

/* converts the given expression from infix to postfix form */
void convert(struct infix *p) {
    char opr;
    
    while (*(p->s)) {
        if (*(p->s) == ' ' || *(p->s) == '\t') {
            p->s++;
            continue;
        }
        
        if (isdigit(*(p->s)) || isalpha(*(p->s))) {
            while (isdigit(*(p->s)) || isalpha(*(p->s))) {
                *(p->t) = *(p->s);
                p->s++;
                p->t++;
            }
        }
        
        if (*(p->s) == '(') {
            push(p, *(p->s));
            p->s++;
        }
        
        if (*(p->s) == '*' || *(p->s) == '+' || *(p->s) == '/' || 
            *(p->s) == '%' || *(p->s) == '-' || *(p->s) == '$') {
            if (p->top != -1) {
                opr = pop(p);
                while (priority(opr) >= priority(*(p->s))) {
                    *(p->t) = opr;
                    p->t++;
                    opr = pop(p);
                }
                push(p, opr);
                push(p, *(p->s));
            }
            else
                push(p, *(p->s));
            p->s++;
        }
        
        if (*(p->s) == ')') {
            opr = pop(p);
            while ((opr) != '(') {
                *(p->t) = opr;
                p->t++;
                opr = pop(p);
            }
            p->s++;
        }
    }
    
    while (p->top != -1) {
        char opr = pop(p);
        *(p->t) = opr;
        p->t++;
    }
    *(p->t) = '\0';
}

/* returns the priority of an operator */
int priority(char c) {
    if (c == '$')
        return 3;
    if (c == '*' || c == '/' || c == '%')
        return 2;
    else {
        if (c == '+' || c == '-')
            return 1;
        else
            return 0;
    }
}

/* displays the postfix form of given expr. */
void show(struct infix p) {
    printf("%s", p.target);
}
```

### Output:
```
Enter an expression in infix form:
4$2*3-3+8/4/(1+1)
Stack is empty
The postfix expression is:
42$3*3-84/11+/+
```

### Explanation

This program contains a structure called `infix`. The elements `target` and `stack` are used to store the postfix string and to maintain the stack respectively. The char pointers `s` and `t` are used to store intermediate results while converting an infix expression to a postfix form. The variable `top` points to the top of the stack.

During program execution when user enters an arithmetic expression the function `setexpr()` assigns the base address of the string to char pointer `s`.

Next, the function `convert()` gets called. This function converts the given infix expression to postfix expression. This function scans every character of the string in a while loop and performs one of the following operations depending on the type of character scanned.

(a) If the character scanned happens to be a space, then that character is skipped.

(b) If character scanned is a digit or an alphabet, it is added to the target string pointed to by `t`.

(c) If the character scanned is a closing parentheses then it is pushed to the stack by calling `push()` function.

(d) If the character scanned is an operator, then firstly, the topmost element from the stack is retrieved. Through a while loop, the priorities of the character scanned (i.e. `*(p->s)`) and the character popped `opr` are compared. Then following steps are performed:
   - (i) If `opr` has higher or same priority as the character scanned, then `opr` is added to the target string.
   - (ii) If `opr` has lower precedence than the character scanned, then the loop is terminated. `opr` is pushed back to the stack. Then, the character scanned (`*(p->s)`) is also pushed to the stack.

(e) If the character scanned is an opening parenthesis, then the continues till it does not encounter a closing parenthesis. The popped operators are added to the target string pointed to by `t`.

In the `convert()` function we have called functions `push()`, `pop()`, `priority()`. The `push()` function adds a character to the stack, whereas the `pop()` function removes the topmost item from the stack. The `priority()` function returns the priority of operators used in the infix expression. `$` (exponentiation) has the highest precedence, followed by `*`, `/` and `+`, `-`. The function returns integer 3 for `$`, 2 for `*` or `/`, 1 for `+` or `-` and 0 for any other character.

The while loop in `convert()` gets terminated if the string `s` is exhausted. By then some operators may still be in the stack. These operators should get added to the postfix string. This is done once the control reaches outside the while loop in the `convert()` function. Lastly, the converted expression is displayed using the `show()` function.

The steps performed in the conversion of a sample infix expression `4$2*3-3+8/4/(1+1)` to a postfix expression are shown in Table 5-1.

### Table 5-1: Conversion of Infix to Postfix

| Char Scanned | Stack Contents | Postfix Expression |
|--------------|----------------|-------------------|
| 4 | Empty | 4 |
| $ | $ | 4 |
| 2 | $ | 4 2 |
| * | * | 4 2 $ |
| 3 | * | 4 2 $ 3 |
| - | - | 4 2 $ 3 * |
| 3 | - | 4 2 $ 3 * 3 |
| + | + | 4 2 $ 3 * 3 - |
| 8 | + | 4 2 $ 3 * 3 - 8 |
| / | + / | 4 2 $ 3 * 3 - 8 |
| 4 | + / | 4 2 $ 3 * 3 – 8 4 |
| / | + / | 4 2 $ 3 * 3 – 8 4 / |
| ( | + / ( | 4 2 $ 3 * 3 – 8 4 / |
| 1 | + / ( | 4 2 $ 3 * 3 – 8 4 / 1 |
| + | + / ( + | 4 2 $ 3 * 3 – 8 4 / 1 |
| 1 | + / ( + | 4 2 $ 3 * 3 – 8 4 / 1 1 |
| ) | + / | 4 2 $ 3 * 3 – 8 4 / 1 1 + |
| | Empty | 4 2 $ 3 * 3 – 8 4 / 1 1 + / + |

---