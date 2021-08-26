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
    2. [Split a sequence in an optimal way (LC1335)][Minimum Difficulty of a Job Schedule]:


2. How to realize that a problem is NOT a dynamic programming problem? 
    1. [One way to realize that it isn't dynamic programming][LC1631. Path With Minimum Effort] is to notice that the hiker can go in all four directions. This means that a dp algorithm would need to look into subproblems that haven't been solved yet.




[LC1631. Path With Minimum Effort]: https://leetcode.com/problems/path-with-minimum-effort/solution/
[Minimum Difficulty of a Job Schedule]: https://leetcode.com/problems/minimum-difficulty-of-a-job-schedule/