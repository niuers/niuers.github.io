---
title: "Robot Bounded In Circle (LC1041)"
date: 2021-07-19
categories:
  - blog
tags:
  - algorithm
  - leetcode
---

1. Experience:
    1. When I was reading the problem, I didn't have much clue how to work it out. Except that I know if after some iterations, the robot goes back to the origin (with the same direction), then it's in a circle. I don't know how to do this problem.
    2. After reading the solution, it turns out that one needs to do some math work beforehand. Basically, we need to prove the following fact:
        1. After at most 4 cycles, any limit cycle trajectory returns to the initial point x = 0, y = 0. That is related to the fact that 4 directions (north, east, south, west) define the repeated cycles' plane symmetry.
        2. However we do not need to run 4 cycles to identify the limit cycle trajectory. One cycle is enough. There could be two situations here.
            * First, if the robot returns to the initial point after one cycle, that's the limit cycle trajectory.
            * Second, if the robot doesn't face north at the end of the first cycle, that's the limit cycle trajectory. Once again, that's the consequence of the plane symmetry for the repeated cycles.
        3. If you assign `north, west, south, east = 0,1,2,3` and assume each cycle moves `dx, dy`, you can prove the above claims.



2. How did I or Other people get the solution? 

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
* [LC1041. Robot Bounded In Circle][LeetCode Link]


[LeetCode Link]: https://leetcode.com/problems/car-fleet-ii/