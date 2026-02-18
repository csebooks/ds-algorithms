---
title: 'Big θ Notation'
weight: 20
references:
    books:
        - b1:
            title: Data Structures and Algorithm Analysis in C by Mark Allen Weiss 
            url: https://mrajacse.files.wordpress.com/2012/08/data-structures-and-algorithm-analysis-in-c-mark-allen-weiss.pdf
        - b2:
            title: Data_Structures_and_Algorithm_Analysis_2e By mark-allen-weiss
            url: https://www.google.co.in/books/edition/Data_Structures_and_Algorithm_Analysis_i/83RWbPynhkgC?hl=en&gbpv=1
---

Big θ gives the **tightest lower bound and tightest upper bound** of growth rate of an algorithm. Thus, if rate of growth of an algorithm is represented by a function f(n) and there is another function g(n) = n², then **θ(g(n))** or **θ(n²)** means:
`c₁g(n) <= f(n) <= c₂g(n)`

where c₁ and c₂ are some constants > 0 and n >= n₀ >= 1.

Thus, if there are positive constants n₀, c₁ and c₂ such that at and to the right of n₀, value of f(n) always is bounded by g(n) on either side. Thus, Big θ indicates that the time complexity of an algorithm will at least be c₁.g(n) and will not be poorer than c₂.g(n). This category is usually not of interest to us.

### Summary:
- **Big O** tells us the **maximum** time complexity (worst case)
- **Big Ω** tells us the **minimum** time complexity (best case)
- **Big θ** tells us **both**

They are not to be confused with worst-case input, best-case input and average-case input discussed in the later section.

Thus, asymptotic notations allow us to compare and rank the growth rate or order of growth of an algorithm.

---
