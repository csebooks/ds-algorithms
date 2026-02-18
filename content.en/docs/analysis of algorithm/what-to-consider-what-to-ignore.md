---
title: 'What to Consider, What to Ignore?'
weight: 14
references:
    books:
        - b1:
            title: Data Structures and Algorithm Analysis in C by Mark Allen Weiss 
            url: https://mrajacse.files.wordpress.com/2012/08/data-structures-and-algorithm-analysis-in-c-mark-allen-weiss.pdf
        - b2:
            title: Data_Structures_and_Algorithm_Analysis_2e By mark-allen-weiss
            url: https://www.google.co.in/books/edition/Data_Structures_and_Algorithm_Analysis_i/83RWbPynhkgC?hl=en&gbpv=1
---

It is very important to decide which operations to consider and which operations to ignore while analyzing an algorithm. For this we must first identify which is the significant time-consuming operation(s) in the algorithm. Once that is decided, we should determine which of these operations are integral to the algorithm and which merely contribute to the overheads.

There are two classes of operations that are typically chosen for the significant operation—**comparison** or **arithmetic**.

For example, in **Searching and Sorting algorithms** the important task being done is the comparison of two values. While searching, the comparison is done to check if the value in a set matches the one we are looking for, whereas in sorting the comparison is done to see whether values being compared are out of order.

The arithmetic operations fall under two groups—**additive** and **multiplicative**.
- **Additive operators** include: addition, subtraction, increment, and decrement.
- **Multiplicative operators** include: multiplication, division, and exponentiation.

### Example: Counting characters in a file

**Algorithm:**
```text
1: Count = 0
2: While (condition – is there a character available for reading from file)
3:   do
4:     Increment Count by 1
5:     Get the next character
6: End while
7: Print Count
```

If there are 500 characters present in the file, then number of times each step is performed would be as follows:

| Step | Operation | Count |
|------|-----------|-------|
| 1 | Initialize count | 1 |
| 2 | Conditional checks | 500 + 1 (+1 is for last check) |
| 4 | Increment Count | 500 |
| 5 | Get next character | 500 |
| 7 | Print Count | 1 |

As can be seen from these numbers, conditional checks, the number of increments and get next character are far too many as compared to number of initialization and printing operations. The number of initialization and printing operations would remain same for a file of any size and they become a much smaller percentage of the total as the file size increases. For a large file, the number of initialization and printing operations would be insignificant as compared to the number of increments and conditional checks. Thus, while analyzing this algorithm the initialization and printing operation should be ignored and only steps 2, 4 and 5 should be considered.

---
