---
title: 'Applications of Priority Queues'
weight: 4
---

## Applications of Priority Queues

We have already mentioned how priority queues are used in operating systems design. In Chapter 9, we will see how priority queues are used to implement several graph algorithms efficiently. Here we will show how to use priority queues to obtain solutions to two problems.

### The Selection Problem

The first problem we will examine is the selection problem from Chapter 1. Recall that the input is a list of n elements, which can be totally ordered, and an integer k. The selection problem is to find the kth largest element.

Two algorithms were given in Chapter 1, but neither is very efficient. The first algorithm, which we shall call Algorithm 1A, is to read the elements into an array and sort them, returning the appropriate element. Assuming a simple sorting algorithm, the running time is O(n2). The alternative algorithm, 1B, is to read k elements into an array and sort them. The smallest of these is in the kth position. We process the remaining elements one by one. As an element arrives, it is compared with kth element in the array. If it is larger, then the kth element is removed, and the new element is placed in the correct place among the remaining k - 1 elements. When the algorithm ends, the element in the kth position is the answer. The running time is O(n k) (why?). If k = n/2, then both algorithms are O(n2). Notice that for any k, we can solve the symmetric problem of finding the (n - k + 1)th smallest element, so k = n/2 is really the hardest case for these algorithms. This also happens to be the most interesting case, since this value of k is known as the median.

We give two algorithms here, both of which run in O(n log n) in the extreme case of k = n/2 , which is a distinct improvement.

#### Algorithm 6A

For simplicity, we assume that we are interested in finding the kth smallest element. The algorithm is simple. We read the n elements into an array. We then apply the build_heap algorithm to this array. Finally, we'll perform k delete_min operations. The last element extracted from the heap is our answer. It should be clear that by changing the heap order property, we could solve the original problem of finding the kth largest element.

The correctness of the algorithm should be clear. The worst-case timing is O(n) to construct the heap, if build_heap is used, and O(log n) for each delete_min. Since there are k delete_mins, we obtain a total running time of O(n + k log n). If k = O(n/log n), then the running time is dominated by the build_heap operation and is O(n). For larger values of k, the running time is O(k log n). If k = n/2 , then the running time is (n log n).

Notice that if we run this program for k = n and record the values as they leave the heap, we will have essentially sorted the input file in O(n log n) time. In Chapter 7, we will refine this idea to obtain a fast sorting algorithm known as heapsort.

#### Algorithm 6B

For the second algorithm, we return to the original problem and find the kth largest element. We use the idea from Algorithm 1B. At any point in time we will maintain a set S of the k largest elements. After the first k elements are read, when a new element is read, it is compared with the kth largest element, which we denote by Sk. Notice that Sk is the smallest element in S. If the new element is larger, then it replaces Sk in S. S will then have a new smallest element, which may or may not be the newly added element. At the end of the input, we find the smallest element in S and return it as the answer.

This is essentially the same algorithm described in Chapter 1. Here, however, we will use a heap to implement S. The first k elements are placed into the heap in total time O(k) with a call to build_heap. The time to process each of the remaining elements is O(1), to test if the element goes into S, plus O(log k), to delete Sk and insert the new element if this is necessary. Thus, the total time is O(k + (n - k) log k) = O (n log k) . This algorithm also gives a bound of (n log n) for finding the median.

In Chapter 7, we will see how to solve this problem in O(n) average time. In Chapter 10, we will see an elegant, albeit impractical, algorithm to solve this problem in O(n) worst-case time.

### Event Simulation

In Section 3.4.3, we described an important queuing problem. Recall that we have a system, such as a bank, where customers arrive and wait on a line until one of k tellers is available. Customer arrival is governed by a probability distribution function, as is the service time (the amount of time to be served once a teller is available). We are interested in statistics such as how long on average a customer has to wait or how long the line might be.

With certain probability distributions and values of k, these answers can be computed exactly. However, as k gets larger, the analysis becomes considerably more difficult, so it is appealing to use a computer to simulate the operation of the bank. In this way, the bank officers can determine how many tellers are needed to ensure reasonably smooth service.

A simulation consists of processing events. The two events here are (a) a customer arriving and (b) a customer departing, thus freeing up a teller.

We can use the probability functions to generate an input stream consisting of ordered pairs of arrival time and service time for each customer, sorted by arrival time. We do not need to use the exact time of day. Rather, we can use a quantum unit, which we will refer to as a tick.

One way to do this simulation is to start a simulation clock at zero ticks. We then advance the clock one tick at a time, checking to see if there is an event. If there is, then we process the event(s) and compile statistics. When there are no customers left in the input stream and all the tellers are free, then the simulation is over.

The problem with this simulation strategy is that its running time does not depend on the number of customers or events (there are two events per customer), but instead depends on the number of ticks, which is not really part of the input. To see why this is important, suppose we changed the clock units to milliticks and multiplied all the times in the input by 1,000. The result would be that the simulation would take 1,000 times longer!

The key to avoiding this problem is to advance the clock to the next event time at each stage. This is conceptually easy to do. At any point, the next event that can occur is either (a) the next customer in the input file arrives, or (b) one of the customers at a teller leaves. Since all the times when the events will happen are available, we just need to find the event that happens nearest in the future and process that event.

If the event is a departure, processing includes gathering statistics for the departing customer and checking the line (queue) to see whether there is another customer waiting. If so, we add that customer, process whatever statistics are required, compute the time when that customer will leave, and add that departure to the set of events waiting to happen.

If the event is an arrival, we check for an available teller. If there is none,we place the arrival on the line (queue); otherwise we give the customer a teller, compute the customer's departure time, and add the departure to the set of events waiting to happen.

The waiting line for customers can be implemented as a queue. Since we need to find the event nearest in the future, it is appropriate that the set of departures waiting to happen be organized in a priority queue. The next event is thus the next arrival or next departure (whichever is sooner); both are easily available.

It is then straightforward, although possibly time-consuming, to write the simulation routines. If there are C customers (and thus 2C events) and k tellers, then the running time of the simulation would be O(C log(k + 1)) because computing and processing each event takes O(logH), where H = k + 1 is the size of the heap.

We use O(C log(k + 1)) instead of O(C log k) to avoid confusion for the k = 1 case.
