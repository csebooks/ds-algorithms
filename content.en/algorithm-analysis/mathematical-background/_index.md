---
title: 'Mathematical Background'
weight: 1
---

[comment]: <> (katex Header)
{{< katex display >}}{{< /katex >}}

# Mathematical Background

The analysis required to estimate the resource use of an algorithm is generally a theoretical issue, and therefore a formal framework is required. We begin with some mathematical definitions.

Throughout the book we will use the following four definitions:

**DEFINITION:** 
T(n) = O(f(n)) if there are constants c and n0 such that T(n) cf (n) when n  n0.

**DEFINITION:**
 T(n) = (g(n)) if there are constants c and n0 such that T(n) cg(n) when n n 0

**DEFINITION:** 
 T(n) = (h(n)) if and only if T(n) = O(h(n)) and T(n) = (h(n)).

**DEFINITION:** 
T(n) = o(p(n)) if T(n) = O(p(n)) and T(n) (p(n)).

The idea of these definitions is to establish a relative order among functions. Given two functions, there are usually points where one function is smaller than the other function, so it does not make sense to claim, for instance, f(n) < g (n). Thus, we compare their relative rates of growth. When we apply this to the analysis of algorithms, we shall see why this is the important measure.

Although 1,000n is larger than n2 for small values of n, n2 grows at a faster rate, and thus n2 will eventually be the larger function. The turning point is n = 1,000 in this case. The first definition says that eventually there is some point n0 past which c f (n) is always at least as large as T(n), so that if
constant factors are ignored, f(n) is at least as big as T(n). In our case, we have T(n) = 1,000n, f(n) = n2, n0 = 1,000, and c = 1. We could also use n0 = 10 and c = 100. Thus, we can say that 1,000n = O(n2) (order n-squared). This notation is known as Big-Oh notation. Frequently, instead of saying "order . . . ," one says "Big-Oh . . . ."

If we use the traditional inequality operators to compare growth rates, then the first definition says that the growth rate of T(n) is less than or equal to () that of f(n). The second definition, T(n) = (g(n)) (pronounced "omega"),says that the growth rate of T(n) is greater than or equal to () that of g(n). The third definition, T(n) = (h(n)) (pronounced "theta"), says that the growth rate of T(n) equals (=) the growth rate of h(n). The last definition, T (n) = o(p(n)) (pronounced "little-oh"), says that the growth rate of T(n) is less than (<) the growth rate of p(n). This is different from Big-Oh, because Big-Oh allows the possibility that the growth rates are the same.

When we say that T(n) = O(f(n)), we are guaranteeing that the function T(n) grows at a rate no faster than f(n); thus f(n) is an upper bound on T(n). Since this implies that f(n) = (T(n)), we say that T(n) is a lower bound on f(n).

As an example, n3 grows faster than n2, so we can say that n2 = O(n3) or n3 = (n2). f(n) = n2 and g(n) = 2n2 grow at the same rate, so both f(n) = O(g(n)) and f(n) = (g(n)) are true. When two functions grow at the same rate, then the decision whether or not to signify this with () can depend on the particular context. Intuitively, if g(n) = 2n2, then g(n) = O(n4), g(n) = O(n3), and g(n) = O(n2) are all technically correct, but obviously the last option is the best answer. Writing g(n) = (n2) says not only that g(n) = O(n2), but also that the result is as good (tight) as possible.

The important things to know are

RULE 1:
```
If T1(n) = O(f(n)) and T2(n) = O(g(n)), then

(a) T1(n) + T2(n) = max (O(f(n)), O(g(n))),

(b) T1(n) * T2(n) = O(f(n) * g(n)),

```

Function  -->  Name

--------------------

c --> Constant

logn  -->Logarithmic

log2n --> Log-squared

n  -->   Linear

n  -->   log n

n2  -->  Quadratic

n3  -->  Cubic

2n  -->  Exponential

Figure 2.1 Typical growth rates

RULE 2:
```
If T(x) is a polynomial of degree n, then T(x) = (x^n).
```
RULE 3:

logk n = O(n) for any constant k. This tells us that logarithms grow very slowly.

To see that rule 1(a) is correct, note that by definition there exist four constants c1, c2, n1, and n2 such that T1(n) c1 f(n) for n n1 and T2(n) c2g(n) for n n2. Let n0 = max(n1, n2). Then, for n n0, T1(n) c1f(n) and T2(n) c~2~g(n), so that T1(n) + T2(n) c1f(n) + c2g(n). Let c3 = max

(c1, c2). Then,
```
T1(n) + T2(n)
- c3f(n) + c3g(n)
- c3(f(n) + g(n))
- 2c3 max(f(n), g(n))
- c max(f(n), g(n))

for c = 2c3 and n n0.
```
We leave proofs of the other relations given above as exercises for the reader. This information is sufficient to arrange most of the common functions by growth rate (see Fig. 2.1).

Several points are in order. First, it is very bad style to include constants or low-order terms inside a Big-Oh. Do not say T(n) = O(2n2) or T(n) = O(n2 + n). In both cases, the correct form is T(n) = O(n2). This means that in any analysis that will require a Big-Oh answer, all sorts of shortcuts are possible. Lower- order terms can generally be ignored, and constants can be thrown away. Considerably less precision is required in these cases.

Secondly, we can always determine the relative growth rates of two functions f(n) and g(n) by computing limn f(n)/g(n), using L'Hôpital's rule if necessary.*

*L'Hôpital's rule states that if limn f(n) = and limn g(n), then limn f(n)/g(n) = limn f'(n) / g'(n), where f'(n) and g'(n)

are the derivatives of f(n) and g(n), respectively.
```
The limit can have four possible values:
- The limit is 0: This means that f(n) = o(g(n)).

- The limit is c 0: This means that f(n) = (g(n)).

- The limit is : This means that g(n) = o(f(n)).

- The limit oscillates: There is no relation (this will not happen in our context).
```
Using this method almost always amounts to overkill. Usually the relation between f(n) and g(n) can be derived by simple algebra. For instance, if f(n) = n log n and g(n) = n1.5, then to decide which of f(n) and g(n) grows faster, one really needs to determine which of log n and n0.5 grows faster. This is like determining which of log2 n or n grows faster. This is a simple problem, because it is already known that n grows faster than any power of a log. Thus, g(n) grows faster than f(n).

One stylistic note: It is bad to say f(n) O(g(n)), because the inequality is implied by the definition. It is wrong to write f(n) O(g(n)), which does not make sense.