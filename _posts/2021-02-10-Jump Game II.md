---
title: "Jump Game II"
date: 2021-02-09
categories:
  - blog
tags:
  - algorithm
  - leetcode
  - dynamic programming
---

1. Experience:
    1. I wrote a dynamic program solution to solve the problem in `O(n^2)` complexity. I went backward from the last element. At each index, I compute the minimum step needed to jump from current index to the last index. I have to figure out what's the minimum steps in all indices after current index to find the new minimum. 
    This way, the algorithm has to be `O(n^2)`.
    2. I tried different ways to reduce the time complexity without any luck.
    3. After reading the solution, it turns out that a better solution is achieved by using greedy algorithm. It is very tricky and I don't quite understand the algorithm and I am not sure how to prove that it always arrives in the minimum jumps.
    4. *Update*: In my 2nd time trying on this problem, I still didn't come up with the greedy solution :(


2. How did I get the solution? 


3. Different solutions
    1. Backtracking
    2. Dynamic Programming
    3. Greedy

4. Mistakes

5. Problem Type

6. Similar Problems



7. Template



Resources:
* [Jump Game II][LeetCode Link]

[LeetCode Link]: https://leetcode.com/problems/jump-game-ii/