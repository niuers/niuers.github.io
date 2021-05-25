---
title: "Number Of Corner Rectangles (LC750)"
date: 2021-05-22
categories:
  - blog
tags:
  - algorithm
  - leetcode
---

1. Experience:
    1. I first tried a brutal force solution, where I go through each cell and for each of them, I check if it can be a top-left corner of a rectangle. This takes `O(m^2n^2)` and clearly I got TLE.
    2. I then tried to improve the algorithm. I noticed that on each cell of 1, I can count along its row and col axis, how many horizontal and vertical line segments have fallen on the axes. The segments are defined by two `1`. So if I know the number of these, I can compute the rectangles as the number of intersection of these two sets.
    3. This somehow is not straightforward to implement. I spent a lot of time to make the implementation correct, but I still got TLE in the end. 

2. How did I or Other people get the solution? 
    1. Other people are processing the grid row by row. Whereas I was thinking about processing them cell by cell, which makes the implementation complicate. My method is also dynamic programming based, i.e. meoization. But requires two sets of data in row and column directions, while other people's solutions only need consider rows, which makes it simpler to implement.
    2. Also, my solution doesn't improve on the time complexity neither due to the `O(n)` set union operation. 

3. Different solutions

4. Mistakes

5. Problem Type
    
6. Similar Problems

7. Template

8. I understand the solution, but HOW do I think to GET there myself?
    1. Where could you improve?
        1. Next time, if I see some solution is too complicate, I should try to change the gear, restart from brutal force and change direction of thinking. 

    2. What questions should I ask myself so that I push myself closer to the solution? 
        1. I should ask myself about the time complexity of brutal force and all the algorithms I tried to implement. Try do it step by step if I can't figure out the optimal solution at the first time. 
    3. What conclusions did I reach that I dropped some idea for the other?
    4. How can I reach this conclusion faster ?
    



Resources:
* [750. Number of Corner Rectangles][LeetCode Link]


[LeetCode Link]: https://leetcode.com/problems/number-of-corner-rectangles/