---
title: "Max Points on a Line (LC149)"
date: 2021-03-16
categories:
  - blog
tags:
  - algorithm
  - leetcode
---

1. Experience:
    1. I started with brutal force method. Try to list all possible lines that can be formed by the points.
    2. To achieve this, I check all possible pairs of the points and compute the line corresponding to the two points. I use a hash dictionary to count the number of points.
    3. Need to pay attention to:
        * What is the key for the dictionary?
        * I used the difference of x and y, i.e. `(dx,dy)`, but it's not unique unless I do fraction simplification. However, the problem doesn't say that the numbers are all integers. So I can't do this.
        * I have to use `(slope, intercept)` format. Need to deal with special cases where the line is vertical.
        * Also, I was trying to count the points directly at first. However, there might be double counts because a point can be on a line with more than one points before it. So it can be counted twice. I ended up using set to avoid double counting.
        * Need consider the case when there's only 1 point.


2. How did I or Other people get the solution? 


3. Different solutions


4. Mistakes
    1. It turns out that they do consider the representation problem of floating point numbers. So they did try to simplify the fraction and use co-prime numbers as the key.
    2. They use `math.gcd` to find out the co-primes
5. Problem Type
    
6. Similar Problems


7. Template

8. I understand the solution, but HOW do I think to GET there myself?
    1. Where could you improve?
        * I mostly relied on test cases to find out bugs in my solution. I should try harder to debug on paper.
    2. What questions should I ask myself so that I push myself closer to the solution? 
    3. What conclusions did I reach that I dropped some idea for the other? 
    4. How can I reach this conclusion faster ?
    



Resources:
* [149. Max Points on a Line][LeetCode Link]


[LeetCode Link]: https://leetcode.com/problems/max-points-on-a-line/