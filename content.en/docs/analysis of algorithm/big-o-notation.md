---
title: 'Big O Notation'
weight: 18
references:
    books:
        - b1:
            title: Data Structures and Algorithm Analysis in C by Mark Allen Weiss 
            url: https://mrajacse.files.wordpress.com/2012/08/data-structures-and-algorithm-analysis-in-c-mark-allen-weiss.pdf
        - b2:
            title: Data_Structures_and_Algorithm_Analysis_2e By mark-allen-weiss
            url: https://www.google.co.in/books/edition/Data_Structures_and_Algorithm_Analysis_i/83RWbPynhkgC?hl=en&gbpv=1
---

If rate of growth of an algorithm is **n²** then using Big O notation, it is said that time complexity of the algorithm is **O(n²)**. What this means is, in the worst case this algorithm's growth rate would be n². It might be slightly better than n² (say n or n log n), but it would never be worse than n². Thus, Big O gives the tightest (closest) upper bound for the rate of growth of the algorithm in question. Though not correct strictly, in common parlance people loosely say that this algorithm will take **n²** time to execute.

### Mathematical Definition:

If rate of growth of an algorithm is represented by a function f(n) and there is another function g(n) = n², then **O(g(n))** or **O(n²)** means:
`f(n) <= c × g(n)`

where c is some constant > 0 and n >= n₀ >= 1.

Thus, if there are positive constants n₀ and c such that at and to the right of n₀, value of f(n) always lies on or below g(n).

**Big O is a very popular way of representing time or space complexity of an algorithm**, as it gives a clear idea of how worse the algorithm would perform, and no more.

---
