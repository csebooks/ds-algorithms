---
title: 'Types of Input to Consider During Analysis'
weight: 24
references:
    books:
        - b1:
            title: Data Structures and Algorithm Analysis in C by Mark Allen Weiss 
            url: https://mrajacse.files.wordpress.com/2012/08/data-structures-and-algorithm-analysis-in-c-mark-allen-weiss.pdf
        - b2:
            title: Data_Structures_and_Algorithm_Analysis_2e By mark-allen-weiss
            url: https://www.google.co.in/books/edition/Data_Structures_and_Algorithm_Analysis_i/83RWbPynhkgC?hl=en&gbpv=1
---

Choosing the input to consider when analyzing an algorithm can have a significant impact on how an algorithm will perform. For example, if the input list is already sorted, some sorting algorithms will perform very well, but other sorting algorithms may perform very poorly. The opposite may be true if the list is randomly arranged instead of sorted.
Hence, multiple input sets must be considered while analyzing an algorithm:

### (a) Best Case Input
This represents the input set that allows an algorithm to perform quickest, i.e., with this input the algorithm takes shortest time to execute, as it causes the algorithms to do the least amount of work.
Example: For a searching algorithm the best case would be if the value we are searching for is found in the first location that the search algorithm checks. As a result, this algorithm would need only one comparison irrespective of the complexity of the algorithm.
Since possibility of best-case input for an algorithm would usually be very small, the best-case analysis of an algorithm is often not done.

### (b) Worst Case Input
This represents the input set that allows an algorithm to perform slowest. Worst case is an important analysis because it gives us an idea of the maximum time an algorithm will ever take. Worst case analysis requires that we identify the input values that cause an algorithm to do the most work.
Example: For a searching algorithm, the worst case is one where the value is in the last place we check or is not in the list. This could involve comparing the key to each list value for a total of N comparisons.

### (c) Average Case Input
This represents the input set that allows an algorithm to deliver an average performance. Average-case analysis is a four-step process:
1. Determine the number of different groups into which all possible input sets can be divided.
2. Determine the probability that the input will come from each of these groups.
3. Determine how long the algorithm will run for each of these groups. All of the input in each group should take the same amount of time, and if they do not, the group must be split into two separate groups.
4. Calculate average case time using the formula:

`A(n) = Σ(i=1 to m) pᵢ × tᵢ`

Where:
n = Size of input
m = Number of groups
pᵢ = Probability that the input will be from group i
tᵢ = Time that the algorithm takes for input from group i

Note that Big O, Big Ω and Big θ can be computed for all the three types of input case mentioned above.
