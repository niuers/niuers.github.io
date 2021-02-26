---
title: "Largest Rectangle in Histogram (LC84)"
date: 2021-02-16
categories:
  - blog
tags:
  - algorithm
  - leetcode
  - stack
---

1. Experience:
    1. I can write out the brutal force solution
    2. It's hard to think about the `O(nlogn)` and `O(n)` case.

2. How did I get the solution? 


3. Different solutions
    1. Divide and Conquer: Think about the minimum height between any two indices. Check for the cases where the minimum height belongs to the maximum area or not. What is a `O(logn)` way to find the minimum height? Segment tree? I am not familiar with it though.
    2. A bar is either in the maximum area or not, we can compute the maximum possible area formed using current bar's height. Do this for each bar and we can get the maximum area. It seems easier to compute the area by fixing the height.


4. Mistakes

5. Problem Type
    * Stack
    * Divide and Conquer

6. Similar Problems



7. Template



Resources:
* [84. Largest Rectangle in Histogram][LeetCode Link]

[LeetCode Link]: https://leetcode.com/problems/largest-rectangle-in-histogram/