---
title: "Range Sum Query 2D - Mutable (LC308)"
date: 2021-03-23
categories:
  - blog
tags:
  - algorithm
  - leetcode
  - Binary Index Tree
  - Segment Tree
---

1. Experience:
    1. I didn't implement the brutal force solution.
    2. I tried to be smarter:
        1. I pre-computed all the sums from `[0][0]` to all other entries.
        2. I save the values of the matrix
        3. I used a dictionary to save the updates
            * The key is row number
            * The value is another dictionary, which has column as key and the change of value (not the value itself) as value
    3. So my update() method is `O(1)`
    4. The sumRegion() only has to deal with entries that have update. Unlesee it's extreme case, `O(mn)`, otherwise it's better.
    5. Luckily, it got accepted.


2. How did I or Other people get the solution? 
    1. They use Binary Index Tree or Segment Tree, which I am not familiar with and they are of lower priority.

3. Different solutions


4. Mistakes

5. Problem Type
    
6. Similar Problems

7. Template

8. I understand the solution, but HOW do I think to GET there myself?
    1. Where could you improve?
    2. What questions should I ask myself so that I push myself closer to the solution? 
    3. What conclusions did I reach that I dropped some idea for the other?
    4. How can I reach this conclusion faster ?
    



Resources:
* [308. Range Sum Query 2D - Mutable][LeetCode Link]


[LeetCode Link]: https://leetcode.com/problems/range-sum-query-2d-mutable/