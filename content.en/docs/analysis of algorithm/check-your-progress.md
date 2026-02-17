---
title: 'Check Your Progress'
weight: 28
references:
    books:
        - b1:
            title: Data Structures and Algorithm Analysis in C by Mark Allen Weiss 
            url: https://mrajacse.files.wordpress.com/2012/08/data-structures-and-algorithm-analysis-in-c-mark-allen-weiss.pdf
        - b2:
            title: Data_Structures_and_Algorithm_Analysis_2e By mark-allen-weiss
            url: https://www.google.co.in/books/edition/Data_Structures_and_Algorithm_Analysis_i/83RWbPynhkgC?hl=en&gbpv=1
---

### Exercise - Level I

**[A] Pick up the correct alternative for each of the following questions:**

**(a) If algorithm A1 is asymptotically more efficient than algorithm A2, then which of the following statement is correct?**
- [ ] A1 would be more efficient for all inputs
- [ ] A1 would be more efficient for all inputs except small inputs
- [ ] A1 would be more efficient for all inputs except large inputs
- [ ] A2 would be more efficient for small inputs

**(b) The correct increasing order of Asymptotic complexity of 4 functions given below is:**
- fun1(n) = 2ⁿ
- fun2(n) = n^(3/2)
- fun3(n) = n log n
- fun4(n) = n^(log n)

**Options:**
- [ ] fun3, fun2, fun4, fun1
- [ ] fun3, fun2, fun1, fun4
- [ ] fun2, fun3, fun1, fun4
- [ ] fun2, fun3, fun4, fun1

**(c) Four functions fun1(), fun2(), fun3() and fun4() use four different for loops given below, where n > 0.**
1. `for (i = 0; i < n; i++)`
2. `for (i = 0; i < n; i += 2)`
3. `for (i = 1; i < n; i *= 2)`
4. `for (i = n; i > -1; i /= 2)`

**Which function would be most efficient?**
- [ ] fun1
- [ ] fun2
- [ ] fun3
- [ ] fun4

**(d) Which of the following is not O(n²)?**
- [ ] 125*n + 12099
- [ ] n^3.14
- [ ] 310*n
- [ ] n³/√n

**(e) Consider the following function fun():**
```c
double fun(int n) {
    int i;
    double sum;
    if (n == 0)
        return 1.0;
    else {
        sum = 0.0;
        for (i = 0; i < n; i++)
            sum += fun(i);
        return sum;
    }
}
```
**The time complexity of the above function is:**
- [ ] O(1)
- [ ] O(n)
- [ ] O(n!)
- [ ] O(nⁿ)

**(f) Consider the following function with n >= m:**
```c
int gcd(int n, int m) {
    if (n % m == 0)
        return m;
    n = n % m;
    return gcd(m, n);
}
```
**How many recursive calls are made in the above function?**
- [ ] θ(log n)
- [ ] Ω(n)
- [ ] θ(log log n)
- [ ] θ(sqrt(n))

**(g) Consider the following pseudo code. What is the total number of multiplications to be performed?**
```text
D = 2
for i = 1 to n do
    for j = 1 to n do
        for k = j+1 to n do
            D = D * 2
```
- [ ] Half of the product of the 3 consecutive integers
- [ ] One-third of the product of the 3 consecutive integers
- [ ] One-sixth of the product of the 3 consecutive integers
- [ ] None of the above

**[B] Two different procedures are written for a given problem. One has a computing time given by 2ⁿ and that for the other is n³. Specify the range of n for which each would be suitable.**

**[C] Compare the two functions n² and 2ⁿ/4 for various values for n. Determine when the second becomes larger than the first.**

**[D] Which of the following function grow faster?**
i. √n or log n?
ii. n^(log n) or (log n)ⁿ?
Prove your claim.

### Sharpen Your Skills
#### Exercise - Level II

**[E] Determine the time complexity of the following algorithms:**

**(a)**
```c
fun(int n) {
    int old, new, term, n;
    old = new = 1;
    printf("%d %d ", old, new);
    for (i = 1; i <= n; i++) {
        term = old + new;
        printf("%d ", term);
        old = new;
        new = term;
    }
}
```

**(b)**
```c
fun(int n) {
    for (i = 1; i <= n; i++) {
        for (j = 1; j <= i; j++) {
            for (k = 1; k <= j; k++)
                printf("Hello\n");
        }
    }
}
```

**(c)**
```c
fun(int n) {
    i = 1;
    while (i <= n) {
        x++;
        i++;
    }
}
```

**(d)**
```c
int fun(int n) {
    int i, j, count = 0;
    for (i = n; i > 0; i /= 2) {
        for (j = 0; j < i; j++)
            count = count + 1;
    }
    return count;
}
```

**(e)**
```c
int fun(int n) {
    int i, j, count = 0;
    for (i = 0; i < n; i++) {
        for (j = i; j > 0; j--)
            count = count + 1;
    }
    return count;
}
```

**(f)**
```c
fun(int n) {
    int i, j = 0;
    for (i = 0; i < n; ++i) {
        while (j < n)
            j++;
    }
}
```

**(g)**
```c
int fun(int n) {
    int i, j, k = 0;
    for (i = n / 2; i <= n; i++) {
        for (j = 2; j <= n; j = j * 2)
            k = k + n / 2;
    }
    return k;
}
```

**(h)**
```c
fun(int n) {
    int j;
    j = 1;
    while (j <= n) {
        j = j * 2;
        printf("Hello\n");
    }
}
```

**(i)**
```c
fun(int n) {
    int i, j;
    for (i = n, j = 0; i > 0; i /= 2, j += i)
        printf("Hello\n");
}
```

**(j)**
```c
fun(int n) {
    int i, j, k;
    for (i = 1; i <= n; i++)
        for (j = i; j <= n; j++)
            for (k = j + 1; k <= n; k++)
                printf("Hello\n");
}
```

**(k)**
```c
fun(int n) {
    int i, j, k;
    for (i = 1; i <= n; i++) {
        for (j = 1; j <= i * i; j++) {
            for (k = 1; k <= n / 2; k++)
                printf("Hello\n");
        }
    }
}
```

**(l)**
```c
fun(int n) {
    int i, j, k;
    for (i = n / 2; i <= n; i++) {
        for (j = 1; j <= n / 2; j++) {
            for (k = 1; k <= n; k = k * 2)
                printf("Hello\n");
        }
    }
}
```

**(m)**
```c
fun(int n) {
    int i, j, k;
    for (i = n / 2; i <= n; i++)
        for (j = 1; j <= n; j = 2 * j)
            for (k = 1; k <= n; k = k * 2)
                printf("Hello\n");
}
```

**(n)**
```c
fun(int n) {
    // Assume n >= 2
    int i, j, k;
    while (n > 1)
        n = n / 2;
}
```

**(o)**
```c
fun(int n) {
    int i, j;
    for (i = 1; i <= n; i++) {
        for (j = 1; j <= n; j = j + i)
            printf("Hello\n");
    }
}
```

**(p)**
```c
fun() {
    int i, j, n, k;
    n = 2^k;
    for (i = 1; i <= n; i++) {
        j = 2;
        while (j <= n) {
            j = j * j;
            printf("Hello\n");
        }
    }
}
```

**[F] Arrange the following functions in ascending order of their growth rate:**
1. fun1 = 2ⁿ
2. fun2 = n^(3/2)
3. fun3 = n log n
4. fun4 = n^(log n)

**[G] Arrange the following functions in ascending order of their growth rate:**
1. fun1 = n^0.99999 log n
2. fun2 = 10000000n
3. fun3 = 1.000001ⁿ
4. fun4 = n²

**[H] Arrange the following functions in increasing asymptotic order:**
1. fun1 = n^(1/3)
2. fun2 = eⁿ
3. fun3 = n^(7/4)
4. fun4 = n log₉n
5. fun5 = 1.0000001ⁿ

**[I] Determine which of the following function is faster:**
- f(n) = n³ for 0 < n < 10000, n² for n >= 10000
- g(n) = n for 0 < n < 100, n³ for n > 100

**[J] Match the following pairs:**

| A | B |
|---|---|
| A. Constant time complexity | 1. O(n!) |
| B. Exponential time complexity | 2. O(1) |
| C. Slowest time | 3. O(2ⁿ) |
| D. Polynomial time complexity | 4. O(nᶜ) |
| E. Big O for 5log n | 5. O(n²) |
| F. Big O for (n log n + n²)(n³ + 2) | 6. O(n² log n) |
| G. Big-O for 2log(n!) + (n² + 1)log n | 7. O(n) |

### Coding Interview Questions
#### Exercise Level III

**For each of the following pairs of functions f(n) and g(n), either f(n) = O(g(n)) or g(n) = O(f(n)) but not both. Determine which the case is for each of the following pairs:**

(a) f(n) = (n² - n)/2, g(n) = 6n
(b) f(n) = n + 2ⁿ, g(n) = n²
(c) f(n) = n + n log n, g(n) = n√n
(d) f(n) = n² + 3n + 4, g(n) = n³
(e) f(n) = n log n, g(n) = n√n
(f) f(n) = n + log n, g(n) = √n
(g) f(n) = 2(log n)², g(n) = log n + 1
(h) f(n) = 4n log n + n, g(n) = (n² - n)/2
(i) f(n) = n + 2√n, g(n) = n²

### Case Scenario Exercise
#### Growth rates
**List the following functions from highest to lowest order. If any are of the same order, circle them on your list.**

`2ⁿ, n log log n, n³ + log n, log n, n² + 5n, 3²ⁿ⁻¹, n², 2ⁿ, n³, n log n, (log n)², n, 6n!, n, (3/2)ⁿ`
