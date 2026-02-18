---
title: 'Why Analyze Algorithms?'
weight: 3
references:
    books:
        - b1:
            title: Data Structures and Algorithm Analysis in C by Mark Allen Weiss 
            url: https://mrajacse.files.wordpress.com/2012/08/data-structures-and-algorithm-analysis-in-c-mark-allen-weiss.pdf
        - b2:
            title: Data_Structures_and_Algorithm_Analysis_2e By mark-allen-weiss
            url: https://www.google.co.in/books/edition/Data_Structures_and_Algorithm_Analysis_i/83RWbPynhkgC?hl=en&gbpv=1
---

Now important part.

**Analysis of algorithm** means checking:

- ⏱ How much time it takes  
- 💾 How much memory it uses  

Mainly we focus on:

1. **Time Complexity**
2. **Space Complexity**

or small inputs, almost all programs look fast.

## Why Do We Need It?

But what if input size becomes:

- 10
- 1,000
- 1,00,000
- 10,00,000

Some algorithms become very slow as input grows.

So we analyze to know:

- Will it scale?
- Will it handle large data?
- Is it efficient?

---

# Time Complexity

Time complexity tells:

> How running time increases when input size (n) increases.

We measure growth using **Big-O Notation**.