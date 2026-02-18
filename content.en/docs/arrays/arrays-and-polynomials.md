---
title: Arrays and Polynomials
weight: 7
---

Polynomials like 5X⁴ + 2X³ + 7X² + 10X - 8 can be maintained using an array. The simplest way to represent a polynomial of degree n is to store the coefficient of (n+1) terms of a polynomial in an array. For this each element of the array should consist of two values—coefficient and exponent. While storing the polynomial it is assumed that the exponent of each successive term is less than that of the previous term. Once we build an array to represent a polynomial, we can use it to perform common polynomial operations like addition and multiplication. The following program demonstrates how we can store polynomials and add them.

### Honest Solid Code
**Program 2-3. Implementation of polynomial addition**

```c
#include <stdio.h>
#define MAX 10

struct term
{
    int coeff;
    int exp;
};

struct poly
{
    struct term t[10];
    int noofterms;
};

void initpoly(struct poly *);
void polyappend(struct poly *, int c, int e);
struct poly polyadd(struct poly, struct poly);
void display(struct poly);

int main()
{
    struct poly p1, p2, p3;
    
    initpoly(&p1);
    initpoly(&p2);
    initpoly(&p3);
    
    polyappend(&p1, 1, 7);
    polyappend(&p1, 2, 6);
    polyappend(&p1, 3, 5);
    polyappend(&p1, 4, 4);
    polyappend(&p1, 5, 2);
    
    polyappend(&p2, 1, 4);
    polyappend(&p2, 1, 3);
    polyappend(&p2, 1, 2);
    polyappend(&p2, 1, 1);
    polyappend(&p2, 2, 0);
    
    p3 = polyadd(p1, p2);
    
    printf("First polynomial:\n");
    display(p1);
    printf("Second polynomial:\n");
    display(p2);
    printf("Resultant polynomial:\n");
    display(p3);
    
    return 0;
}

/* initializes elements of struct poly */
void initpoly(struct poly *p)
{
    int i;
    p->noofterms = 0;
    for (i = 0; i < MAX; i++)
    {
        p->t[i].coeff = 0;
        p->t[i].exp = 0;
    }
}

/* adds the term of polynomial to the array t */
void polyappend(struct poly *p, int c, int e)
{
    p->t[p->noofterms].coeff = c;
    p->t[p->noofterms].exp = e;
    (p->noofterms)++;
}

/* displays the polynomial equation */
void display(struct poly p)
{
    int flag = 0, i;
    for (i = 0; i < p.noofterms; i++)
    {
        if (p.t[i].exp != 0)
            printf("%d x^%d + ", p.t[i].coeff, p.t[i].exp);
        else
        {
            printf("%d", p.t[i].coeff);
            flag = 1;
        }
    }
    if (!flag)
        printf("\b\b ");
    printf("\n");
}

/* adds two polynomials p1 and p2 */
struct poly polyadd(struct poly p1, struct poly p2)
{
    int i, j, c;
    struct poly p3;
    
    initpoly(&p3);
    
    if (p1.noofterms > p2.noofterms)
        c = p1.noofterms;
    else
        c = p2.noofterms;
    
    for (i = 0, j = 0; i <= c; p3.noofterms++)
    {
        if (p1.t[i].coeff == 0 && p2.t[j].coeff == 0)
            break;
        
        if (p1.t[i].exp >= p2.t[j].exp)
        {
            if (p1.t[i].exp == p2.t[j].exp)
            {
                p3.t[p3.noofterms].coeff = p1.t[i].coeff + p2.t[j].coeff;
                p3.t[p3.noofterms].exp = p1.t[i].exp;
                i++;
                j++;
            }
            else
            {
                p3.t[p3.noofterms].coeff = p1.t[i].coeff;
                p3.t[p3.noofterms].exp = p1.t[i].exp;
                i++;
            }
        }
        else
        {
            p3.t[p3.noofterms].coeff = p2.t[j].coeff;
            p3.t[p3.noofterms].exp = p2.t[j].exp;
            j++;
        }
    }
    return p3;
}
```

**Output:**
```
First polynomial:
1 x^7 + 2 x^6 + 3 x^5 + 4 x^4 + 5 x^2 
Second polynomial:
1 x^4 + 1 x^3 + 1 x^2 + 1 x^1 + 2
Resultant polynomial:
1 x^7 + 2 x^6 + 3 x^5 + 5 x^4 + 1 x^3 + 6 x^2 + 1 x^1 + 2
```

In this program the structure `poly` contains another structure element of the type `struct term`. This structure stores the coefficient and exponent of the term of a polynomial. The element `noofterms` stores the total number of terms that a variable of the type `struct poly` is supposed to hold. The function `polyappend()` adds the term of a polynomial to the array `t`. The function `polyadd()` adds the polynomials represented by variables `p1` and `p2`. The function `display()` displays the polynomial.

In `main()`, we have called the function `polyappend()` several times to build two polynomials represented by variables `p1` and `p2`. Next, the function `polyadd()` is called. While doing so we have passed `p1` and `p2` and collected their sum in `p3`. In this function, arrays representing the two polynomials are traversed. While traversing, the polynomials are compared on a term-by-term basis. If the exponents of the two terms being compared are equal then their coefficients are added and the result is stored in the third polynomial. If the exponents of two terms are not equal then the term with the bigger exponent is added to the third polynomial. If the term with an exponent is present in only one of the two polynomials, then that term is added as it is to the third polynomial.

Lastly, the terms of the resulting polynomial are displayed using the function `display()`.

---