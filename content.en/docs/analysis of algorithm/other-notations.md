---
title: 'Other Notations'
weight: 21
references:
    books:
        - b1:
            title: Data Structures and Algorithm Analysis in C by Mark Allen Weiss 
            url: https://mrajacse.files.wordpress.com/2012/08/data-structures-and-algorithm-analysis-in-c-mark-allen-weiss.pdf
        - b2:
            title: Data_Structures_and_Algorithm_Analysis_2e By mark-allen-weiss
            url: https://www.google.co.in/books/edition/Data_Structures_and_Algorithm_Analysis_i/83RWbPynhkgC?hl=en&gbpv=1
---

Apart from Big O, Big Ω and Big θ, there are two more notations:

| Notation | Description |
|----------|-------------|
| **Little o** | Used to describe an upper bound that **cannot be tight**. In other words, loose upper bound of function f(n). In asymptotic notation: `f(n) < c × g(n)` |
| **Little ω** | Used to describe a **loose lower bound** of f(n). In asymptotic notation: `f(n) > c × g(n)` |

Since both these notations give loose upper or lower bound, they are not commonly used to represent the time or space complexity of an algorithm.

---
