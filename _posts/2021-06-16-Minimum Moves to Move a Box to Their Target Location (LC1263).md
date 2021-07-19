---
title: "Minimum Moves to Move a Box to Their Target Location (LC1263)"
date: 2021-06-16
categories:
  - blog
tags:
  - algorithm
  - leetcode
  - dynamic programming
---

1. Experience:
    1. I started with the correct solution but missed some subtle points.
        * It's possible that a path is no longer usable after the box is moved to some place.
        * It's possible that we can move back to the same grid point (but push from another direction) to get to the target.
            * This indicates change of state for my visited set. However, I didn't get it. I was trying to use previous location as another condition to check, which didn't pass the test cases. (TLE)


2. How did I or Other people get the solution? 

3. Different solutions

4. Mistakes


5. Problem Type


  
6. Similar Problems

7. Template

8. I understand the solution, but HOW do I think to GET there myself?
    1. Where could you improve?
        * Thinking of allowing visited set to have a state which is expanded version of just point coordinates.
    2. What questions should I ask myself so that I push myself closer to the solution? 
    3. What conclusions did I reach that I dropped some idea for the other?
    4. How can I reach this conclusion faster ?
    



Resources:
* [1263. Minimum Moves to Move a Box to Their Target Location][LeetCode Link]


[LeetCode Link]: https://leetcode.com/problems/minimum-moves-to-move-a-box-to-their-target-location/