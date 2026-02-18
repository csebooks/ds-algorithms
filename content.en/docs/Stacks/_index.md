---
title: 'Stacks'
weight: 5
references:
    books:
        - b1:
            title: Data Structures and Algorithm Analysis in C by Mark Allen Weiss 
            url: https://mrajacse.files.wordpress.com/2012/08/data-structures-and-algorithm-analysis-in-c-mark-allen-weiss.pdf
        - b2:
            title: Data_Structures_and_Algorithm_Analysis_2e By mark-allen-weiss
            url: https://www.google.co.in/books/edition/Data_Structures_and_Algorithm_Analysis_i/83RWbPynhkgC?hl=en&gbpv=1

---

# Chapter 5: Stacks

## Of Wads Of Notes

### Why This Chapter Matters?

Be it items in a store, books in a library, or notes in a bank, the moment they become more than handful we start stacking them neatly. Similarly, while maintaining data in an orderly fashion it is placed in a stack. Stack data structure is used widely for storing variables, managing function calls, evaluating arithmetic expressions, etc. Hence it is important to understand this data structure.

---

Stack is a data structure in which addition of new element or deletion of an existing element always takes place at the same end. This end is known as **top of stack**. This situation can be compared to a stack of plates in a cafeteria where every new plate added to the stack is added at the top. Similarly, every new plate taken off the stack is also from the top of the stack. When an item is added to a stack, the operation is called **push**, and when an item is removed from the stack the operation is called **pop**. These operations are shown in Figure 5-1. Because of the nature of push and pop operations Stack is also called **last-in-first-out (LIFO)** list.

![Figure 5-1: Insertion and deletion of elements in a Stack](image-placeholder)

A stack data structure can be maintained as an array or as a linked list. The following sections discuss these implementations.

---

## Stack as an Array

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

## Stack as a Linked List

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

## Applications of Stacks

Stacks are often used in evaluation of arithmetic expression. An arithmetic expression consists of operands and operators. The operands can be constant or variables. The operators used in an arithmetic expression can be `+`, `-`, `*` and `/`.

While writing an arithmetic expression, the operator is placed between two operands as shown in the examples below.

```
A + B * C
A * B - C
A + B / C - D
A $ B + C
```

This way of representing arithmetic expressions is called **infix notation**. While evaluating an infix expression usually the following operator precedence is used:

| Priority | Operators |
|----------|-----------|
| Highest | Exponentiation ($) |
| Next highest | Multiplication (*) and Division (/) |
| Lowest | Addition (+) and Subtraction (-) |

If we wish to override these priorities we can do so by using a pair of parentheses as shown below.

```
(A + B) * C
A * (B - C)
(A + B) / (C - D)
```

The expressions within a pair of parentheses are always evaluated earlier than other operations.

To make evaluation of an arithmetic expression easy, a polish mathematician Jan Lukasiewicz suggested a notation called **Polish notation**. As per this notation, an expression in infix form can be converted to either **prefix** or **postfix** form and then evaluated. In **prefix notation** the operator comes before the operands. In **postfix notation**, the operator follows the two operands. These forms are shown below.

| Infix | Prefix | Postfix |
|-------|--------|---------|
| A + B | + A B | A B + |

The prefix and postfix expressions have three features:
- The operands maintain the same order as in the equivalent infix expression
- Parentheses are not needed to designate the expression unambiguously.
- While evaluating the expression the priority of the operators is irrelevant.

The stack data structure is used while carrying out the conversion of an expression given in one form to another.

---

## Infix to Postfix Conversion

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

## Postfix to Prefix Conversion

Let us now see a program that converts an expression in postfix form to a prefix form.

---

### Program 5-4: Postfix to Prefix conversion

```c
#include <stdio.h>
#include <string.h>

#define MAX 50

struct postfix {
    char stack[MAX][MAX], target[MAX];
    char temp1[2], temp2[2];
    char str1[MAX], str2[MAX], str3[MAX];
    int i, top;
};

void initpostfix(struct postfix *);
void setexpr(struct postfix *, char *);
void push(struct postfix *, char *);
void pop(struct postfix *, char *);
void convert(struct postfix *);
void show(struct postfix);

int main() {
    struct postfix q;
    char expr[MAX];
    
    initpostfix(&q);
    printf("Enter an expression in postfix form:\n");
    gets(expr);
    setexpr(&q, expr);
    convert(&q);
    printf("The Prefix expression is:\n");
    show(q);
    
    return 0;
}

/* initializes the elements of the structure */
void initpostfix(struct postfix *p) {
    p->i = 0;
    p->top = -1;
    strcpy(p->target, "");
}

/* copies given expr. to target string */
void setexpr(struct postfix *p, char *c) {
    strcpy(p->target, c);
}

/* adds an operator to the stack */
void push(struct postfix *p, char *str) {
    if (p->top == MAX - 1)
        printf("Stack is full\n");
    else {
        p->top++;
        strcpy(p->stack[p->top], str);
    }
}

/* pops an element from the stack */
void pop(struct postfix *p, char *a) {
    if (p->top == -1)
        printf("Stack is empty\n");
    else {
        strcpy(a, p->stack[p->top]);
        p->top--;
    }
}

/* converts given expr. to prefix form */
void convert(struct postfix *p) {
    while (p->target[p->i] != '\0') {
        /* skip whitespace, if any */
        if (p->target[p->i] == ' ')
            p->i++;
        
        if (p->target[p->i] == '%' || p->target[p->i] == '-' ||
            p->target[p->i] == '/' || p->target[p->i] == '*' ||
            p->target[p->i] == '+' || p->target[p->i] == '$') {
            pop(p, p->str2);
            pop(p, p->str3);
            p->temp1[0] = p->target[p->i];
            p->temp1[1] = '\0';
            strcpy(p->str1, p->temp1);
            strcat(p->str1, p->str3);
            strcat(p->str1, p->str2);
            push(p, p->str1);
        }
        else {
            p->temp1[0] = p->target[p->i];
            p->temp1[1] = '\0';
            strcpy(p->temp2, p->temp1);
            push(p, p->temp2);
        }
        p->i++;
    }
}

/* displays the prefix form of expr. */
void show(struct postfix p) {
    char *temp = p.stack[0];
    while (*temp) {
        printf("%c ", *temp);
        temp++;
    }
}
```

### Output:
```
Enter an expression in postfix form:
42$3*3-84/11+/+
The Prefix expression is:
+ - * $ 4 2 3 3 / / 8 4 + 1 1
```

### Explanation

In this program the structure `postfix` contains character arrays like `temp1`, `temp2`, `str1`, `str2`, `str3` to store the intermediate results. The character arrays `stack` and `target` are used to maintain the stack and to store the final string in the prefix form respectively.

In the `convert()` function the string containing expression in postfix form is scanned through a while loop till the string target is not exhausted. Following steps are performed depending on the type of character scanned.

(a) If the character scanned is a space, then that character is skipped.

(b) If the character scanned contains a digit or an alphabet, it is pushed to the stack by calling `push()` function.

(c) If the character scanned contains an operator, then the topmost two elements are popped from the stack. These two elements are then stored in the array `temp1`. A temporary string `temp2` containing the operator and the two operands is formed. This temporary string is then pushed on the stack.

The converted prefix form is stored at the 0th position in the stack. Finally, the `show()` function displays this prefix form. The steps performed in the conversion of a sample postfix expression `4 2 $ 3 * 3 - 8 4 / 1 1 + / +` to its equivalent prefix expression is shown in Table 5-2.

### Table 5-2: Conversion of Postfix to Prefix

| Char. Scanned | Stack Contents |
|---------------|----------------|
| 4 | 4 |
| 2 | 4, 2 |
| $ | $ 4 2 |
| 3 | $ 4 2, 3 |
| * | * $ 4 2 3 |
| 3 | * $ 4 2 3, 3 |
| - | - * $ 4 2 3 3 |
| 8 | - * $ 4 2 3 3, 8 |
| 4 | - * $ 4 2 3 3, 8, 4 |
| / | - * $ 4 2 3 3, / 8 4 |
| 1 | - * $ 4 2 3 3, / 8 4, 1 |
| 1 | - * $ 4 2 3 3, / 8 4, 1, 1 |
| + | - * $ 4 2 3 3, / 8 4, + 1 1 |
| / | - * $ 4 2 3 3, / / 8 4 + 1 1 |
| + | + - $ 4 2 3 3 / / 8 4 + 1 1 |

---

## Other Inter-Conversions

We have seen conversion of infix to postfix form and postfix to prefix form. It is also possible to carry out other conversions as well. Figure 5-3 summarizes the operations to be performed to carry out these interconversions.

![Figure 5-3: Summary of inter-conversion of expressions](image-placeholder)

---

## Evaluation of Postfix Expression

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

## Exercise - Level I

### [A] Fill in the blanks:

(a) A stack is a data structure in which addition of new element or deletion of an existing element always takes place at an end called ______.

(b) The data structure stack is also called _____________ list.

(c) In __________ notation the operator precedes the two operands.

(d) In __________ notation the operator follows the two operands.

### [B] Pick up the correct alternative for each of the following questions:

(a) Adding an element to the stack means
   1. Placing an element at the front end
   2. Placing an element at the top
   3. Placing an element at the rear end
   4. None of the above

(b) Pushing an element to a stack means
   1. Removing an element from the stack
   2. Searching a given element in the stack
   3. Adding a new element to the stack
   4. Sorting the elements in the stack

(c) Popping an element from the stack means
   1. Removing an element from the stack
   2. Searching a given element in the stack
   3. Adding a new element to the stack
   4. Sorting the elements in the stack

(d) The expression A B *
   1. is an infix expression
   2. is a postfix expression
   3. is a prefix expression
   4. is a stack expression

---

## Sharpen Your Skills: Exercise - Level II

### [C] Transform the following infix expressions into their equivalent postfix expressions:

1. `(A - B) * (D / E)`
2. `(A + B ^ D) / (E - F) + G`
3. `A * (B + D) / E - F * (G + H / K)`
4. `(A + B) * (C - D) $ E * F`
5. `(A + B) * (C $(D - E) + F) / G) $ (H - J)`

### [D] Transform the following infix expressions into their equivalent prefix expressions:

1. `(A - B) * (D / E)`
2. `(A + B ^ D) / (E - F) + G`
3. `A * (B + D) / E - F * (G + H / K)`

### [E] Transform each of the following prefix expression to infix:

1. `+ A - B C`
2. `+ + A - * $ B C D / + E F * G H I`
3. `+ - $ A B C * D ** E F G`

### [F] Transform each of the following postfix expression to infix:

1. `A B C + -`
2. `A B - C + D E F - + $`
3. `A B C D E - + $ * E F * -`

---

## Coding Interview Questions: Exercise Level III

### [G] Write programs for the following:

(a) Copying contents of one stack to another

(b) To check whether in a string containing an arithmetic expression, the opening and closing parenthesis are well-formed or not

---

## Case Scenario Exercise: Prefix to postfix and infix forms

Write a program to convert an arithmetic expression in prefix form to equivalent infix and postfix forms. Refer Figure 5-4 for the steps to be carried out in each of these conversions.
```