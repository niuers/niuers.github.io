---
title: "Elimination Game (LC390)"
date: 2021-03-10
categories:
  - blog
tags:
  - algorithm
  - leetcode
  - dynamic programming
  - math
---

1. Experience:
    1. I first wrote a brutal force solution, where I do exactly as the problem specifies: go through each element, eliminate the every other one, put the rest into a new array, reverse it and do the process again. Without a doubt, the solution got TLE. This one has `O(n^2)` time complexity.
    2. I realized that I can reuse the previously computed remaining number if I consider the location only. That is, for a given size of array, regardless of the numbers in the array, the one left is always in a fixed location. If I have a larger array, each time it'll reduce to half of the size, then I can reuse the remaining location found for the smaller array size.
        * So I use an array to save the remaining location for a given array size. 
        * I tried to loop from `1 to n` and compute the remaining location for each of them. To make the program simple, I create the new array each time, and use its size to find the remaining location from previous calculations.
        * This still gives me TLE, it has a complexity of `O(n^2)` since I have to create new array each time.
        * I found out that the only thing matters is the size of the array, I don't really need to construct new array each time, so I remove that part of code. The size of new array can be found directly through the size of current array. I now have a solution of `O(n)` complexity. However, it still got a TLE. 
    3. I realized that there must be a `O(logn)` solution, which prompts me to think about binary algorithm. It's clear that each time, the array size is halved, so this can be the key here.
        * For ease of implementation, I chose to use recursive method. Each time, I'll only need compute the remaining location for half of the current array size. 
        * Now I have a `O(logn)` time complexity solution and it got accepted with 68% ranking.

2. How did I or Other people get the solution? 


3. Different solutions
    1. People found that for numbers `1,2,...,n`. The sum of remaining number from left to right and remaining number from right to left equals to `n+1`. This can be used to compute the result easily since after first elimination, all even numbers are left, if you divide the numbers by 2, then you get another array with size `n//2`.
    2. People also found some patterns on how the `head` of array moves when we move from left to right and right to left.




4. Mistakes

5. Problem Type

6. Similar Problems
  1. 


7. Template



Resources:
* [390. Elimination Game][LeetCode Link]


[LeetCode Link]: https://leetcode.com/problems/elimination-game/