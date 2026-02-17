---
title: 'Determining Time Complexity'
weight: 23
references:
    books:
        - b1:
            title: Data Structures and Algorithm Analysis in C by Mark Allen Weiss 
            url: https://mrajacse.files.wordpress.com/2012/08/data-structures-and-algorithm-analysis-in-c-mark-allen-weiss.pdf
        - b2:
            title: Data_Structures_and_Algorithm_Analysis_2e By mark-allen-weiss
            url: https://www.google.co.in/books/edition/Data_Structures_and_Algorithm_Analysis_i/83RWbPynhkgC?hl=en&gbpv=1
---

From the Asymptotic Analysis discussed previously, we know that we would be interested in **Big O** as it represents the worst-case time complexity. Let us determine the time complexity of programmatic implementation of some algorithms.

### Example 1-9
```c
fun() {
    int i;
    for (i = 1 to n)
        printf("Hello\n");
}
```
Here printf() would be executed n times so time complexity is O(n).

### Example 1-10
```c
fun() {
    int i, j;
    for (i = 1 to n) {
        for (j = 1 to n)
            printf("Hello\n");
    }
}
```
Here printf() would be executed n² times so time complexity is O(n²).

### Example 1-11
```c
fun(int n) {
    int i = 1;
    for (i = 1; i * i <= n; i++)
        printf("Hello\n");
}
```
The condition used in the loop i*i <= n which is same as i <= √n. So printf() would get executed √n times. So time complexity is O(√n).

### Example 1-12
```c
fun(int n) {
    int i = 1, s = 1;
    while (s <= n) {
        i++;
        s = s + i;
        printf("Hello\n");
    }
}
```
Here we can't say that the loop would be executed n times because value of s is being incremented in steps of i and not in steps of 1.

Pattern of values:
i = 1, 2, 3, 4, 5, ..., k
s = 1, 3, 6, 10, 15, 21, ... (sum of first i natural numbers)

When loop stops: s > n

`k(k + 1)/2 > n`
or `(k² + k)/2 > n`
Ignoring the lower order terms: `k² > n`
So, number of iterations k will be √n
Time complexity is O(√n).

### Example 1-13
```c
fun(int n) {
    int i, j, k;
    for (i = 1; i <= n; i++) {
        for (j = 1; j <= i; j++) {
            for (k = 1; k <= 50; k++)
                printf("Hello\n");
        }
    }
}
```
Analysis:
For i = 1, j loop executes 1 time and k loop executes 50 times
For i = 2, j loop executes 2 times and k loop executes 2 × 50 times
For i = 3, j loop executes 3 times and k loop executes 3 × 50 times
...
For i = n, j loop executes n times and k loop executes n × 50 times
So, printf() would get executed:

`50 + 2×50 + 3×50 + ... + n×50 times`
`= 50 × (1 + 2 + 3 + ... + n) times`
`= 50 × n(n + 1)/2 times`

Ignoring the lower order terms and the coefficients, time complexity would be O(n²).

### Example 1-14
```c
fun(int n) {
    int i;
    for (i = 1; i < n; i = i * 2)
        printf("Hello\n");
}
```
In this function the value of i is incremented as: 2⁰, 2¹, 2², 2³, ..., 2ᵏ
When all iterations are over, 2ᵏ would be equal to n. So, k would be equal to log₂n.
So printf() would get executed log₂n times.
Time complexity is O(log₂n).

Note: Had the incrementation been done using i = i * 3, time complexity would be O(log₃n). Likewise, had it been done using i = i * 4, time complexity would be O(log₄n).
