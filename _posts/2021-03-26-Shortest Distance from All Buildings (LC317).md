---
title: "Shortest Distance from All Buildings (LC317)"
date: 2021-03-27
categories:
  - blog
tags:
  - algorithm
  - leetcode
  - BFS
---

1. Experience:
    1. This problem looks similar to another problem also asking for shortest distance from all buildings but without any obstacle. 
        * I thought I can re-use the other problem's solution, where the optimal location is the median of the houses' row and column indexes. 
        * It seems not so straightforward. If the optimal location is occupied by an obstacle, then we have to move to other places to find an empty land.
        * I also thought under what condition there won't be such optimal location. Initially, I thought that if there's one obstacle in each row, then they will divide the grid into two parts, the house in left part can NOT connect to the house in the right part. 
        * This turned out to be wrong, as there can be gaps in the column indexes of these obstacles, where one can avoid next row's obstacle and go to other part.

    2. I didn't think about writing a brutal force solution, as I thought it won't get accepted at all, why bother writing it. 
    3. It turns out I was wrong. The discussion talks about using BFS to find the shortest distance from an empty land to all other houses. 
    4. It's not so straightforward to implement a recursive BFS solution.
    5. I ended with a iterative BFS solution using double deque.
    

2. How did I or Other people get the solution? 


3. Different solutions


4. Mistakes

5. Problem Type
    
6. Similar Problems

7. Template

8. I understand the solution, but HOW do I think to GET there myself?
    1. Where could you improve?
        * If I don't have any clue how to efficiently solve a problem, start with brutal force solution. Write it out and improve upon it.
    2. What questions should I ask myself so that I push myself closer to the solution? 
    3. What conclusions did I reach that I dropped some idea for the other?
    4. How can I reach this conclusion faster ?
    



Resources:
* [317. Shortest Distance from All Buildings][LeetCode Link]


[LeetCode Link]: https://leetcode.com/problems/shortest-distance-from-all-buildings/