---
title: "Parse Expressions"
date: 2021-04-27
categories:
  - blog
tags:
  - algorithm
  - summary
---

1. Dynamic Programming
    1. Typically problems involving finding the "longest/shortest/largest/smallest/maximal" of something have the optimal-substructure.
        * First, the question is asking for the maximum or minimum of something. 
        * Second, we have to make decisions that may depend on previously made decisions, which is very typical of a problem involving subsequences.
    2. [Split a sequence in an optimal way (LC1335)][Minimum Difficulty of a Job Schedule]:


2. How to realize that a problem is NOT a dynamic programming problem? 
    1. [One way to realize that it isn't dynamic programming][LC1631. Path With Minimum Effort] is to notice that the hiker can go in all four directions. This means that a dp algorithm would need to look into subproblems that haven't been solved yet.

3. [Ugly Number][LC264. Ugly Number II]
    1. Since any existed number will be multiplied by 2, 3 and 5 once and only once, otherwise duplicate, we can use a pointer to keep track of where the 2, 3 and 5 are going to multiply in the next step.
    2. Once, we find the next minimum, we can move on the corresponding pointer, otherwise it always stays at the already existed ugly number which would makes pointer useless

4. A Framework to Solve Dynamic Programming Problems
    1. A dynamic programming algorithm typically has 3 components
        1. First, we need some function or array that represents the answer to the problem for a given state. 
        2. Second, we need a way to transition between states, This is called a recurrence relation and figuring it out is usually the hardest part of solving a problem with dynamic programming.
        3. The third component is establishing base cases. 

5. [Longest increasing subsequence][LC300. Longest Increasing Subsequence]
    1. dynamic programming: `O(n^2)`
    2. build up the sequence one by one: `O(n^2)`
        * If using binary search, `O(nlogn)`

[LC1631. Path With Minimum Effort]: https://leetcode.com/problems/path-with-minimum-effort/solution/
[Minimum Difficulty of a Job Schedule]: https://leetcode.com/problems/minimum-difficulty-of-a-job-schedule/
[LC264. Ugly Number II]: https://leetcode.com/problems/ugly-number-ii/
[LC300. Longest Increasing Subsequence]: https://leetcode.com/problems/longest-increasing-subsequence/