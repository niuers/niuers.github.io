---
title: "Largest Divisible Subset (LC368)"
date: 2021-03-08
categories:
  - blog
tags:
  - algorithm
  - leetcode
  - dynamic programming
---

1. Experience:
    1. I started with brutal force solution. How do I enumerate all the cases such that I can find the one with maximum subset size? Here are some observations:
        * If there's such a subset, the maximum number must be divisible by all other numbers, and the 2nd largest number must be divisible by all other numbers except the maximum one, etc. 
        * So it makes sense to sort the original list and start from the largest number first.
        * Note though that the subset with largest number does not necessarily have the largest subset size. 
    2. I wrote a recursive version to solve the problem. For each number, I check the maximum subset size that has the current number as the largest value. Along with the process, I save the maximum subset for each number. 
    3. This turns out to be a dynamic programming problem, with standard memoization technique.
  

2. How did I or Other people get the solution? 


3. Different solutions
    * The other people's solutions look much shorter than mine. 



4. Mistakes

5. Problem Type
    * Dynamic programming

6. Similar Problems
  1. 


7. Template



Resources:
* [368. Largest Divisible Subset][LeetCode Link]


[LeetCode Link]: https://leetcode.com/problems/largest-divisible-subset/