---
title: 'Asymptotic Analysis Examples'
weight: 22
references:
    books:
        - b1:
            title: Data Structures and Algorithm Analysis in C by Mark Allen Weiss 
            url: https://mrajacse.files.wordpress.com/2012/08/data-structures-and-algorithm-analysis-in-c-mark-allen-weiss.pdf
        - b2:
            title: Data_Structures_and_Algorithm_Analysis_2e By mark-allen-weiss
            url: https://www.google.co.in/books/edition/Data_Structures_and_Algorithm_Analysis_i/83RWbPynhkgC?hl=en&gbpv=1
---

### Example 1-6
**If f(n) = 5n + 3 and g(n) = n, can we say f(n) = O(g(n))?**

We can say f(n) = O(g(n)) if we can find some c and n₀ such that:
`f(n) <= c × g(n), where c > 0, n > n₀ >= 1`

Substituting f(n) and g(n):
`5n + 3 <= cn`

This equation is satisfied, for **c = 6** and for all values of **n >= 3**.

**So, for c = 6, n₀ = 3, f(n) = O(n)**

> Note that g(n) can also be n³, n², 2n which grow faster than n, but tightest upper bound is n. So, **f(n) = O(n)**.

---

### Example 1-7
**If f(n) = 5n + 3 and g(n) = n, can we say f(n) = Ω(g(n))?**

We can say f(n) = Ω(g(n)) if we can find some c and n₀ such that:
`f(n) >= c × g(n), c > 0, n > n₀ >= 1`

Substituting f(n) and g(n):
`5n + 3 >= cn`

This equation is satisfied, for **c = 1** and for all values of **n >= 1**.

**So, for c = 1, n₀ = 1, f(n) = Ω(n)**

> Note that g(n) can also be log n or log log n, which grow slower than n. But tightest lower bound is n. So, **f(n) = Ω(n)**.

---

### Example 1-8
**If f(n) = 5n + 3 and g(n) = n, can we say f(n) = θ(g(n))?**

We can say f(n) = θ(g(n)) if we can find some c₁, c₂ and n₀ such that:
`c₁g(n) <= f(n) <= c₂g(n), where c₁, c₂ > 0, n > n₀ >= 1`

Substituting f(n) and g(n):
`c₁n <= 5n + 3 <= c₂n`

This inequality is satisfied, for **c₁ = 1, c₂ = 6** and for all values of **n >= 3**.

**So, for c₁ = 1, c₂ = 6, n₀ = 3, f(n) = θ(g(n))**

---
