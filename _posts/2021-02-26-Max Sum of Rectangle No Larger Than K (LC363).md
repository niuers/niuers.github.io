---
title: "Max Sum of Rectangle No Larger Than K (LC363)"
date: 2021-02-26
categories:
  - blog
tags:
  - algorithm
  - leetcode
  - Kadane's Algorithm
  - Maximum subarray problem
---

1. Experience:
    1. I started with a brutal force solution: For each grid point, treat it as the top left corner of a sub-rectangle, check every possible sub-rectangle and compute the sum within it to find out the maximum sum.
      * For each point, it takes `O(mn)` to compute all sums of sub-rectangles with it as top left corner.
      * The total time complexity is thus `O(m^2n^2)`
      * The coding is straightforward though as I first computed all the subsums of the sub-rectangles with `[0,0]` as top left corner. Then when I move to other grid points, I can re-use these sub-sums to compute the sum of new sub-rectangle easily. For example, is we are to compute the sum between `a[i][j]` and `a[m][n]`. Then it equals to `s[m][n] - s[m][j-1] - s[i-1][n] + s[i-1][j-1]`, where `s[][]` is the sub-sum matrix using `[0,0]` as top left corner.
    2. As I couldn't find a solution that can get better performance, I had to look into the solutions. 
    3. It turns out that I need understand the following to solve this problem efficiently:
      * [Kadane's algorithm][1D Kadane Algorithm]: it solves the problem of finding the maximum subarray sum in a one-dimensional array
      * An `O(nlog(n))` solution to find [the maximum subarray sum less than or equal to `k` in a one-dimensional array][max subarray sum no more than k]. 
      * [To deal with two-dimensional array][2D Kadane Algorithm], we just have to loop through all possible column combinations and call the above subroutine on the sum of columns. This shall produce a `O(n^2 mlog(m))` time complexity.
    4. However, it's not that so simple for python because the algorithm to find the maximum subarray sum less than `k` requires `O(nlog(n))` time in search and insert. There's no built-in data structure in python that satisfy `O(nlog(n))` time complexity in both 'insertion' and 'search'. 
      * Notice although sorted `list` has `O(log(n))` in search, but it takes `O(n)` to insert a new element.
      * `bisect.bisect_left` costs `O(log(n))` but `bisect.insort` costs `O(n)`
      * There's no sorted set data structure in python, notice we have `OrderedDict` from `collections` but, it's not sorted dictionary as it's ordered by isnertion order. There's no `OrderedSet` neither. 
      * I have to resort to third party python module, e.g. [`from sortedcontainers import SortedSet`][SortedSet], which is supported by LeetCode. The time complexity (of insert, search) is however, complicate. It's approximately `O(log(n))` due to the usage of list of list in its implementation. The author's performance comparison seems convincing that it performs well.
      * The other module `blist` (implemented in B+Tree), although has guaranteed `O(log(n))` time complexity, it's not supported in LeetCode, so I couldn't use it. 
    5. The implementation of sub-routine to find maximum subarray sum which is less or equal to `k` is not so straightforward. My first several iterations didn't cover all the test cases. It turned out, that it's better to insert `0` first into the SortedSet.
    6. I noticed that with such sorted set, the performance is not as good as I had expected, even it passed the test cases, the rank is around `25%`. I took a look at the solutions with better performance, it turns out that they use `bisect.insort` and `bisect.bisect_left`, so even though the `insort` has theoretical complexity of `O(n)`, it somehow outperformces the sorted set here. 
      * How to explain to other people is a bigger problem here.

2. How did I or Other people get the solution? 


3. Different solutions




4. Mistakes

5. Problem Type
    * Maximum subarray problem

6. Similar Problems



7. Template



Resources:
* [363. Max Sum of Rectangle No Larger Than K][LeetCode Link]


[LeetCode Link]: https://leetcode.com/problems/max-sum-of-rectangle-no-larger-than-k/
[max subarray sum no more than k]: https://www.quora.com/Given-an-array-of-integers-A-and-an-integer-k-find-a-subarray-that-contains-the-largest-sum-subject-to-a-constraint-that-the-sum-is-less-than-k
[2D Kadane Algorithm]: https://youtu.be/yCQN096CwWM
[1D Kadane Algorithm]: https://en.wikipedia.org/wiki/Maximum_subarray_problem
[SortedSet]: http://www.grantjenks.com/docs/sortedcontainers/sortedset.html