---
title: "Minimum Time to Build Blocks (LC1199)"
date: 2021-07-11
categories:
  - blog
tags:
  - algorithm
  - leetcode
  - dynamic programming
  - Huffman's Algorithm
---

1. Experience:
    1. At the beginning, it's hard for me to clear out the algorithm that works for all the cases. I thought there was some simplification that can be done to reduce the search domain. So I spent lots of time trying to figure out/prove that it's better to split all workers before assign some workers to certain blocks.
    2. It turned out that we need to try to split workers from 1 to the number of current workers to find the minimum number of cost.
    3. After reading the solutions, I was able to write the `O(n^3)` solution, which got TLE. 
    4. The `O(nlogn)` solution is Huffman's algorithm, which I don't want to touch for now. So I'll just leave it there. But the `O(n^2)` solution is interesting as it reduces the `O(n)` search for each `(worker, block)` pair to `O(1)`. This relates to convert a `min-max` problem to `max-min` problem and re-use the dynamic programming table there. 

2. How did I or Other people get the solution? 

3. Different solutions

4. Mistakes


5. Problem Type


  
6. Similar Problems

7. Template

8. I understand the solution, but HOW do I think to GET there myself?
    1. Where could you improve?
        1. When there seems to be a large search range, don't try to spend too much time on mathematics, instead, write out the formula using full search range, and implement the code first. 
        2. After that, start to simplify the search range by re-using previous computed results instead of thinking too much on math.
    2. What questions should I ask myself so that I push myself closer to the solution? 
    3. What conclusions did I reach that I dropped some idea for the other?
    4. How can I reach this conclusion faster ?
    



Resources:
* [LC1199. Minimum Time to Build Blocks][LeetCode Link]

[LeetCode Link]: https://leetcode.com/problems/minimum-time-to-build-blocks/