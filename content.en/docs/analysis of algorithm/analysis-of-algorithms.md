---
title: 'Analysis of Algorithms'
weight: 2
references:
    books:
        - b1:
            title: Data Structures and Algorithm Analysis in C by Mark Allen Weiss 
            url: https://mrajacse.files.wordpress.com/2012/08/data-structures-and-algorithm-analysis-in-c-mark-allen-weiss.pdf
        - b2:
            title: Data_Structures_and_Algorithm_Analysis_2e By mark-allen-weiss
            url: https://www.google.co.in/books/edition/Data_Structures_and_Algorithm_Analysis_i/83RWbPynhkgC?hl=en&gbpv=1
---

One might feel that with faster computers and increasingly cheaper memory space should we bother about speed and space required by an algorithm anymore. **We should.** That is because though the computers have become faster and memory cheaper, the size of data has also grown exponentially. Imagine the tasks like searching a popular web page from 30 trillion web pages, match a sequence in genomic data set, etc. So, unless we chose the right algorithm to work on such huge datasets, we would end up spending more time and space while performing these tasks.

Moreover, analysis of algorithms gives us a scientific basis to determine which algorithm should be chosen to solve the problem. Also, on analyzing algorithms we can communicate to others about the performance or efficiency of an algorithm using a specific notation (discussed later).

This analysis is done by comparing the time and/or space required for executing the algorithms. Often, there is a trade-off between time and space. In this chapter we would analyze algorithms on the basis of time. We would carry out space-based analysis in later chapters.

While doing time-based analysis of algorithms we do not use conventional time units like seconds or minutes required for executing the algorithms. There are two reasons for this:

1. A worse algorithm may take less time units to execute if we move it to a faster computer, or use a more efficient programming language to implement it.
2. We are interested in **relative efficiency** of different algorithms rather than the exact time for execution.

While analyzing an algorithm, it is assumed that all operations take same time units to perform on any computer. So, instead of time units we consider the number of **prominent operations** that are carried out by the algorithm. For example, in a searching algorithm we would try to determine the number of **comparisons** that are done to search a value in a list of values. Or in an algorithm to add two matrices, we might determine the number of arithmetic operations it performs.

Once we identify the prominent operations in an algorithm, we try to build a **function** that relates the number of times these operations are performed to the size of the input. Once these functions are formed for algorithms under consideration, we can compare them by comparing the rate at which the functions grow as the input gets larger.

This growth rate is critical since there are situations where one algorithm needs fewer operations than the other when the input size is small, but many more when the input size becomes large.

### Steps involved in analyzing two algorithms:

```text
┌─────────────┐     ┌─────────────┐
│  Algorithm 1 │     │  Algorithm 2 │
└──────┬──────┘     └──────┬──────┘
       │                     │
       ▼                     ▼
┌─────────────────┐   ┌─────────────────┐
│ Identify        │   │ Identify        │
│ prominent       │   │ prominent       │
│ operations      │   │ operations      │
└────────┬────────┘   └────────┬────────┘
         │                     │
         ▼                     ▼
┌─────────────────┐   ┌─────────────────┐
│ Ignore trivial  │   │ Ignore trivial  │
│ operations      │   │ operations      │
└────────┬────────┘   └────────┬────────┘
         │                     │
         ▼                     ▼
┌─────────────────────────┐   ┌─────────────────────────┐
│ Define a function that  │   │ Define a function that  │
│ relates no. of opns.    │   │ relates no. of opns.    │
│ with input size         │   │ with input size         │
└───────────┬─────────────┘   └───────────┬─────────────┘
            │                             │
            └──────────┬──────────────────┘
                       │
                       ▼
            ┌─────────────────┐
            │   Compare       │
            │   functions     │
            └────────┬────────┘
                     │
                     ▼
            ┌─────────────────┐
            │  Choose better  │
            │   algorithm     │
            └─────────────────┘
```

---
