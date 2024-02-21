---
title: 'A Lower Bound for Simple Sorting Algorithms'
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


## A Lower Bound for Simple Sorting Algorithms

An inversion in an array of numbers is any ordered pair (i, j) having the property that i < j but a[i] > a[j]. In the example of the last section, the input list 34, 8, 64, 51, 32, 21 had nine inversions, namely (34,8), (34,32), (34,21), (64,51), (64,32), (64,21), (51,32), (51,21) and (32,21). Notice that this is exactly the number of swaps that needed to be (implicitly) performed by insertion sort. This is always the case, because swapping two adjacent elements that are out of place removes exactly one inversion, and a sorted file has no inversions. Since there is O(n) other work involved in the algorithm, the running time of insertion sort is O(I + n), where I is the number of inversions in the original file. Thus, insertion sort runs in linear time if the number of inversions is O(n).

We can compute precise bounds on the average running time of insertion sort by computing the average number of inversions in a permutation. As usual, defining average is a difficult proposition. We will assume that there are no duplicate elements (if we allow duplicates, it is not even clear what the average number of duplicates is). Using this assumption, we can assume that the input is some permutation of the first n integers (since only relative ordering is important) and that all are equally likely. Under these assumptions, we have the following theorem:

**THEOREM 7.1.**

The average number of inversions in an array of n distinct numbers is n(n - 1)/4.

PROOF:

For any list, L, of numbers, consider Lr, the list in reverse order. The reverse list of the example is 21, 32, 51, 64, 34, 8. Consider any pair of two numbers in the list (x, y), with y > x. Clearly, in exactly one of L and Lr this ordered pair represents an inversion. The total number of these pairs in a list L and its reverse Lr is n(n - 1)/2. Thus, an average list has half this amount, or n(n - 1)/4 inversions.

This theorem implies that insertion sort is quadratic on average. It also provides a very strong lower bound about any algorithm that only exchanges adjacent elements.

**THEOREM 7.2.**

Any algorithm that sorts by exchanging adjacent elements requires (n2) time on average.

PROOF:

The average number of inversions is initially n(n - 1)/4 = (n2). Each swap removes only one inversion, so (n2) swaps are required.

This is an example of a lower-bound proof. It is valid not only for insertion sort, which performs adjacent exchanges implicitly, but also for other simple algorithms such as bubble sort and selection sort, which we will not describe here. In fact, it is valid over an entire class of sorting algorithms, including those undiscovered, that perform only adjacent exchanges. Because of this, this proof cannot be confirmed empirically. Although this lower-bound proof is rather simple, in general proving lower bounds is much more complicated than proving upper bounds and in some cases resembles voodoo.

This lower bound shows us that in order for a sorting algorithm to run in subquadratic, or o(n2), time, it must do comparisons and, in particular, exchanges between elements that are far apart. A sorting algorithm makes progress by eliminating inversions, and to run efficiently, it must eliminate more than just one inversion per exchange.
