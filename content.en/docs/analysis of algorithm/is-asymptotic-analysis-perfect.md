---
title: 'Is Asymptotic Analysis Perfect?'
weight: 25
references:
    books:
        - b1:
            title: Data Structures and Algorithm Analysis in C by Mark Allen Weiss 
            url: https://mrajacse.files.wordpress.com/2012/08/data-structures-and-algorithm-analysis-in-c-mark-allen-weiss.pdf
        - b2:
            title: Data_Structures_and_Algorithm_Analysis_2e By mark-allen-weiss
            url: https://www.google.co.in/books/edition/Data_Structures_and_Algorithm_Analysis_i/83RWbPynhkgC?hl=en&gbpv=1
---

Suppose two algorithms have rate of growth represented by functions 100n log n and 2n log n respectively. Ignoring the constants order of growth of both algorithms would be n log n. So, both algorithms are asymptotically same. Hence, we can't judge which one is better.
While doing Asymptotic Analysis we always consider input size n greater than some constant value n₀. But, in reality, we may never supply input bigger than n₀. In such cases, an asymptotically slower algorithm may perform better than an asymptotically faster algorithm.
From these examples we can conclude that asymptotic analysis is not perfect, but it still remains the best way available. Hence, it is widely used while analyzing algorithms.
