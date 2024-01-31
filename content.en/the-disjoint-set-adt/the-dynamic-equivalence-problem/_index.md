---
title: 'The Dynamic Equivalence Problem'
weight: 2
---

# The Dynamic Equivalence Problem

Given an equivalence relation ^~^, the natural problem is to decide, for any a and b, if a ^~^ b. If the relation is stored as a two-dimensional array of booleans, then, of course, this can be done in constant time. The problem is that the relation is usually not explicitly, but rather implicitly, defined.

As an example, suppose the equivalence relation is defined over the five-element set {a1, a2, a3, a4, a5}. Then there are 25 pairs of elements, each of which is

either related or not. However, the information a1^~^a2, a3 ^~^ a4, a5 ^~^ a1, a4 ^~^ a2 implies that all pairs are related. We would like to be able to infer this quickly.

The equivalence class of an element a S is the subset of S that contains all the elements that are related to a. Notice that the equivalence classes form a partition of S: Every member of S appears in exactly one equivalence class. To decide if a ^~^ b, we need only to check whether a and b are in the same equivalence class. This provides our strategy to solve the equivalence problem.

The input is initially a collection of n sets, each with one element. This initial representation is that all relations (except reflexive relations) are false. Each set has a different element, so that Si Sj = ; this makes the sets disjoint.

There are two permissible operations. The first is find, which returns the name of the set (that is, the equivalence class) containing a given element. The second operation adds relations. If we want to add the relation a ^~^ b, then we first see if a and b are already related. This is done by performing finds on both a and b and checking whether they are in the same equivalence class. If they are not, then we apply union. This operation merges the two equivalence classes containing a and b into a new equivalence class. From a set point of view, the result of is to create a new set Sk = Si Sj, destroying the originals and preserving the disjointness of all the sets. The algorithm to do this is frequently known as the disjoint set union/find algorithm for this reason.

This algorithm is dynamic because, during the course of the algorithm, the sets can change via the union operation. The algorithm must also operate on-line: When a find is performed, it must give an answer before continuing. Another possibility would be an off-line algorithm. Such an algorithm would be allowed to see the entire sequence of unions and finds. The answer it provides for each find must still be consistent with all the unions that were performed up until the find, but the algorithm can give all its answers after it has seen all the questions. The difference is similar to taking a written exam (which is generally off-line--you only have to give the answers before time expires), and an oral exam (which is on-line, because you must answer the current question before proceeding to the next question).

Notice that we do not perform any operations comparing the relative values of elements, but merely require knowledge of their location. For this reason, we can assume that all the elements have been numbered sequentially from 1 to n and that the numbering can be determined easily by some hashing scheme. Thus, initially we have Si = {i} for i = 1 through n.

Our second observation is that the name of the set returned by find is actually fairly abitrary. All that really matters is that find(x) = find() if and only if x and are in the same set.

These operations are important in many graph theory problems and also in compilers which process equivalence (or type) declarations. We will see an application later.

There are two strategies to solve this problem. One ensures that the find instruction can be executed in constant worst-case time, and the other ensures that the union instruction can be executed in constant worst-case time. It has recently been shown that both cannot be done simultaneously in constant worst- case time.

We will now briefly discuss the first approach. For the find operation to be fast, we could maintain, in an array, the name of the equivalence class for each element. Then find is just a simple O(1) lookup. Suppose we want to perform union (a, b). Suppose that a is in equivalence class i and b is in equivalence class j. Then we scan down the array, changing all is to j. Unfortunately, this scan takes (n). Thus, a sequence of n - 1 unions (the maximum, since then everything is in one set), would take (n2) time. If there are (n2) find operations, this performance is fine, since the total running time would then amount to O(1) for each union or find operation over the course of the algorithm. If there are fewer finds, this bound is not acceptable.

One idea is to keep all the elements that are in the same equivalence class in a linked list. This saves time when updating, because we do not have to search through the entire array. This by itself does not reduce the asymptotic running time, because it is still possible to perform (n2) equivalence class updates over the course of the algorithm.

If we also keep track of the size of each equivalence class, and when performing unions we change the name of the smaller equivalence class to the larger, then the total time spent for n - 1 merges isO (n log n). The reason for this is that each element can have its equivalence class changed at most log n times, since every time its class is changed, its new equivalence class is at least twice as large as its old. Using this strategy, any sequence of m finds and up to n - 1 unions takes at most O(m + n log n) time.

In the remainder of this chapter, we will examine a solution to the union/find problem that makes unions easy but finds hard. Even so, the running time for any sequences of at most m finds and up to n - 1 unions will be only a little more than O(m + n).