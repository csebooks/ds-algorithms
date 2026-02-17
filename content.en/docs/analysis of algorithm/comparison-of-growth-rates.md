---
title: 'Comparison of Growth Rates'
weight: 16
references:
    books:
        - b1:
            title: Data Structures and Algorithm Analysis in C by Mark Allen Weiss 
            url: https://mrajacse.files.wordpress.com/2012/08/data-structures-and-algorithm-analysis-in-c-mark-allen-weiss.pdf
        - b2:
            title: Data_Structures_and_Algorithm_Analysis_2e By mark-allen-weiss
            url: https://www.google.co.in/books/edition/Data_Structures_and_Algorithm_Analysis_i/83RWbPynhkgC?hl=en&gbpv=1
---

Comparison of some growth rates is obvious. For example, we can intuitively say n³ grows faster than n², which grows faster than n. But we may not be so sure when we compare growth rates of function 2ⁿ and n². In such cases, to compare the growth rates we need to follow the steps mentioned below:

1. If anything is common in both functions, cancel it out
2. Take log of both functions and then compare them
3. Replace n with some large value of power of 2
4. Compare the two functions

> **Note:** If functions differ by constant value, then their growth rate is same.

### Example 1-1
**Which of the following two functions has a faster growth rate?**
- $f(n) = 2^n$
- $g(n) = n^2$

| f(n) | g(n) |
|------|------|
| 2ⁿ | n² |
| n log₂2 | 2 log₂n | *Take log of both functions* |
| n | 2 log₂n | |
| 2¹⁰⁰ | 2 log₂2¹⁰⁰ | *Take n = 2¹⁰⁰* |
| 2¹⁰⁰ | 200 | |

**So, f(n) > g(n)**, or growth rate of f(n) is more than that of g(n).

---

### Example 1-2
**Which of the following two functions has a faster growth rate?**
- $f(n) = 3^n$
- $g(n) = 2^n$

| f(n) | g(n) |
|------|------|
| 3ⁿ | 2ⁿ |
| n log₂3 | n log₂2 | *Take log of both sides* |
| log₂3 | log₂2 | |

**So, f(n) > g(n)**

---

### Example 1-3
**Which of the following two functions has a faster growth rate?**
- $f(n) = n^2$
- $g(n) = n log_2n$

| f(n) | g(n) |
|------|------|
| n² | n log₂n |
| n | log₂n | *Cancel out n* |

**So, f(n) > g(n)**

---

### Example 1-4
**Which of the following two functions has a faster growth rate?**
- $f(n) = n$
- $g(n) = (log_2n)^{100}$

| f(n) | g(n) |
|------|------|
| n | (log₂n)¹⁰⁰ |
| log₂n | 100 × log₂log₂n | *Take log of both functions* |
| log₂2¹²⁸ | 100 × log₂log₂2¹²⁸ | *Substitute n = 2¹²⁸* |
| 128 | 100 × log₂128 | |
| 128 | 100 × 7 | |
| 128 | 700 | |

**So, f(n) < g(n)** (for n = 2¹²⁸)

Let us substitute n = 2¹⁰²⁴:
- log₂2¹⁰²⁴ = 100 × log log₂2¹⁰²⁴
- 1024 = 100 × log 1024
- 1024 = 100 × 10
- 1024 > 1000

**So, f(n) > g(n)** after some value of n.

---

### Example 1-5
**Which of the two functions has a faster growth rate?**
- $f(n) = n^{(log n)}$
- $g(n) = n log n$

| f(n) | g(n) |
|------|------|
| log n × log n | log n + log log n | *Take log of both functions* |
| log₂2¹⁰²⁴ × log₂2¹⁰²⁴ | log₂2¹⁰²⁴ + log log₂2¹⁰²⁴ | *Substitute n = 2¹⁰²⁴* |
| 1024 × 1024 | 1024 + 10 | |

**So, f(n) > g(n)**

---
