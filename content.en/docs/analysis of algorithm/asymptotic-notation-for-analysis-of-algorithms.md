---
title: 'Asymptotic Notation for Analysis of Algorithms'
weight: 17
references:
    books:
        - b1:
            title: Data Structures and Algorithm Analysis in C by Mark Allen Weiss 
            url: https://mrajacse.files.wordpress.com/2012/08/data-structures-and-algorithm-analysis-in-c-mark-allen-weiss.pdf
        - b2:
            title: Data_Structures_and_Algorithm_Analysis_2e By mark-allen-weiss
            url: https://www.google.co.in/books/edition/Data_Structures_and_Algorithm_Analysis_i/83RWbPynhkgC?hl=en&gbpv=1
---

Growth rate of operations performed (which reflects the time required) or space required by an algorithm is often called **time complexity** and **space complexity** of an algorithm. Instead of using a naïve way to compare the time/space complexity of two algorithms, we need a scientific way to do so.

**Asymptotic notations** offer this scientific way. They are mathematical notations suggested by Bachmann and Landau to describe limiting behavior of a function when its argument tends to a particular value or infinity. The word asymptotic is used in broad sense to mean an approximate value that gets closer and closer to the truth, when some parameter approaches a limiting value.

### Following Asymptotic notations are commonly used:

| Notation | Name | Description |
|----------|------|-------------|
| **O(f(n))** | Big Oh Notation | Gives an upper bound for a function f(n) to within a constant factor. Also known as Big O or Big Omicron notation. |
| **Ω(f(n))** | Big Omega Notation | Gives a lower bound for a function f(n) to within a constant factor. |
| **θ(f(n))** | Big Theta Notation | Gives bounds for a function f(n) to within a constant factor. |

![Asymptotic representation of functions]()

---
