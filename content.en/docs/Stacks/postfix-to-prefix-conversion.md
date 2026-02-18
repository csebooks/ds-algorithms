---
title: Postfix to Prefix Conversion
weight: 6
---

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