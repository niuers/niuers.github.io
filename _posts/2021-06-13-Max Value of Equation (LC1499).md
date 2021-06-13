---
title: "Max Value of Equation (LC1499)"
date: 2021-06-13
categories:
  - blog
tags:
  - algorithm
  - leetcode
---

1. Experience:
    1. I couldn't find a better way to solve the problem, so I took a look at the solution.


2. How did I or Other people get the solution? 

3. Different solutions
    1. The second solution uses a deque to simulate a 'monotonic stack', basically before you append to a stack, make sure the values are monotonically increasing or decreasing such that the top of the stack always has the maximum or minimum value.
4. Mistakes


5. Problem Type


  
6. Similar Problems

7. Template

8. I understand the solution, but HOW do I think to GET there myself?
    1. Where could you improve?
        1. I knew that in brutal force solution, I can find all pairs of points and compute the value of equation. I didn't implement it.
        If I did, I probably can find that the equation can be simplified if we know the relationship between the x-coordinates. If so, I may find the optimal solution using heap.
        2. When the solution depends on the choice of something, I should think about how to fix one of the variables to make the problem simpler.
    2. What questions should I ask myself so that I push myself closer to the solution? 
    3. What conclusions did I reach that I dropped some idea for the other?
    4. How can I reach this conclusion faster ?
    



Resources:
* [732. My Calendar III][LeetCode Link]


[LeetCode Link]: https://leetcode.com/problems/my-calendar-iii/