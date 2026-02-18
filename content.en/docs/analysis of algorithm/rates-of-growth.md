---
title: 'Rates of Growth'
weight: 15
references:
    books:
        - b1:
            title: Data Structures and Algorithm Analysis in C by Mark Allen Weiss 
            url: https://mrajacse.files.wordpress.com/2012/08/data-structures-and-algorithm-analysis-in-c-mark-allen-weiss.pdf
        - b2:
            title: Data_Structures_and_Algorithm_Analysis_2e By mark-allen-weiss
            url: https://www.google.co.in/books/edition/Data_Structures_and_Algorithm_Analysis_i/83RWbPynhkgC?hl=en&gbpv=1
---

While analyzing algorithms, more than the exact number of operations performed by the algorithm, it is the **rate of increase in number of operations as the size of the problem increases** that is of more importance. This rate of increase is often called the **growth rate** of an algorithm.

In the example in previous section, the exact number of operations is 1503, whereas, the growth rate is **3n + 3**, where n is the number of characters present in the file. The growth rate is represented using a function and is then called **order of the function**.

### Table 1-1: Rate of increase in common algorithm classes

| n | log n | n log n | n² | n³ | 2ⁿ |
|---|-------|---------|----|----|----|
| 1 | 0.0 | 0.0 | 1.0 | 1.0 | 2.0 |
| 2 | 1.0 | 2.0 | 4.0 | 8.0 | 4.0 |
| 5 | 2.3 | 11.6 | 25.0 | 125.0 | 32.0 |
| 10 | 3.3 | 33.2 | 100.0 | 1000.0 | 1024.0 |
| 15 | 3.9 | 58.6 | 225.0 | 3375.0 | 32768.0 |
| 20 | 4.3 | 86.4 | 400.0 | 8000.0 | 1048576.0 |
| 30 | 4.9 | 147.2 | 900.0 | 27000.0 | 1073741824.0 |
| 40 | 5.3 | 212.9 | 1600.0 | 64000.0 | 1099511627776.0 |
| 50 | 5.6 | 282.2 | 2500.0 | 125000.0 | 1125899906842620.0 |

You can observe that there isn't a significant difference in values when the input is small, but once the input value gets large, there are big differences. Hence, while analyzing algorithms, we must consider what happens when the size of the input is large, because small input sets can hide rather dramatic differences.

If the growth rate of an algorithm doesn't change with the size of the input, then the algorithm is called a **constant time algorithm**. On similar lines, there are:
- **Constant (1)**
- **Linear (n)**
- **Logarithmic (log n)**
- **Log linear (n log n)**
- **Quadratic (n²)**
- **Cubic (n³)**
- **Polynomial (nᶜ)**
- **Exponential (cⁿ)** growth rates.

In general, an algorithm whose time (no of operations)/space has a higher growth rate than another algorithm, will eventually take more time/space as compared to the other.

We can arrange the growth rates in increasing order as follows:
`log log n < log n < n < n log n < n² < n³ < 2ⁿ < nⁿ < 2^(2ⁿ)`

The data in Table 1-1 also illustrates that the faster growing functions increase at such a rate that they quickly dominate the slower-growing functions. Hence, if an algorithm's growth rate is a combination of two of these classes, we can safely ignore the slower growing terms.

For example, if the growth rate of an algorithm is **n² + 3n**, then as n increases the term **n²** will grow much faster than the term 3n. So, we can safely discard the term 3n. On discarding the lower order term, what we are left with is called the **order of the function** or **order of the algorithm** whose growth rate the function represents. An algorithm is considered to be more efficient than another if it has a lower order of growth.

The above discussion relates to behavior of an algorithm as regards time for execution. The same discussion can be extended to the space requirements (memory) of an algorithm. Thus, an algorithm whose space requirement grows at the rate **n²** is considered to be better than the one whose space requirements grows at the rate **n³**.

---
