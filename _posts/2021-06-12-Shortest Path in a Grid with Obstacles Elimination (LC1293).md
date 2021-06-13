---
title: "Shortest Path in a Grid with Obstacles Elimination (LC1293)"
date: 2021-06-12
categories:
  - blog
tags:
  - algorithm
  - leetcode
---

1. Experience:
    1. At the very beginning, I thought this problem is not that hard, I just need to use BFS to find the shortest distance to the end point. In the course, I just have to record the number of obstacles and pick the path with the number of obstacles satisfying the condition. 
    2. The solution turned out to be wrong, through the test case, I found that there can be cases where two nodes' next step can fall on the same node, depending on the current number of obstacles on the two nodes, the new node may have different values of the obstacles. We need pick the smallest number of obstacles for the new node.
    3. I made the change with above observation (This is similar to the relaxation in Dijstra's algorithm). How it failed again in a big test case. Not sure what I did wrong, I tried to use DFS without any success.
    4. I then went back to BFS, and tried to reproduce the error with smaller grid. I finally found out that there are other cases related to how I mark the node as visited.
        * When the algorithm is moving along BFS path, it's possible that we need re-visit a node that has been visited before long time ago, but can have a lower number of obstacles in the current path. 
        * Example: 
        ```
        [[0,0,0],[1,1,0],[0,0,0],[0,1,1],[0,0,0],[1,1,0],[0,0,0],[0,1,1],[0,0,0]]
        1
        ```
        * So I shouldn't use a visited set as usual to record the path, instead, whenever I see a node that has a lower number of obstacles than before, I should add it to the queue and visit it.


2. How did I or Other people get the solution? 

3. Different solutions
    1. Another solution is use the number of obstacles together with coordinates when saving into visited set.
4. Mistakes


5. Problem Type



    
6. Similar Problems

7. Template

8. I understand the solution, but HOW do I think to GET there myself?
    1. Where could you improve?
        * Need run more examples when I have an algorithm and see if it works. 
        * Don't start coding until I have some meaningful examples that can pass the algorithm.
    2. What questions should I ask myself so that I push myself closer to the solution? 
    3. What conclusions did I reach that I dropped some idea for the other?
    4. How can I reach this conclusion faster ?
    



Resources:
* [1293. Shortest Path in a Grid with Obstacles Elimination][LeetCode Link]


[LeetCode Link]: https://leetcode.com/problems/shortest-path-in-a-grid-with-obstacles-elimination/