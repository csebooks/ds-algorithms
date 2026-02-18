---
title: 'Big Ω Notation'
weight: 19
references:
    books:
        - b1:
            title: Data Structures and Algorithm Analysis in C by Mark Allen Weiss 
            url: https://mrajacse.files.wordpress.com/2012/08/data-structures-and-algorithm-analysis-in-c-mark-allen-weiss.pdf
        - b2:
            title: Data_Structures_and_Algorithm_Analysis_2e By mark-allen-weiss
            url: https://www.google.co.in/books/edition/Data_Structures_and_Algorithm_Analysis_i/83RWbPynhkgC?hl=en&gbpv=1
---

Big Ω gives the tightest (closest) **lower bound** of growth rate of an algorithm. Thus, if rate of growth of an algorithm is represented by a function f(n) and there is another function g(n) = n², then **Ω(g(n))** or **Ω(n²)** means:
`f(n) >= c × g(n)`

where c is some constant > 0 and n >= n₀ >= 1.

Thus, if there are positive constants n₀ and c such that at and to the right of n₀, value of f(n) always lies on or above g(n).

Big Ω is not very useful as it indicates that f(n) will grow at a minimum rate of **n²**. It might grow even at a worse rate (say n³ or 2ⁿ). Since Big Ω is an indicator of the least rate at which the algorithm complexity will grow, it is not commonly used. Thus, Big Ω gives the **best-case complexity**, i.e., it indicates how much minimum time will it take to execute an algorithm.

---
