---
title: "The Maze III (LC499)"
date: 2021-06-19
categories:
  - blog
tags:
  - algorithm
  - leetcode
  - stack
---

1. Experience:
    1. I initially thought that I can solve this problem by using DFS. I tried to write a DFS which tries every path to the hole and update the minimum number of steps and corresponding path in a class variable. 
        * However, this doesn't work. In a normal DFS, we have a visited set to record the node that has been visited. However in this problem, we may need visit the same node more than once. It's possible that there are multiple paths from the source to this node and each path will have different distance. As DFS doesn't visit node by its distance to the source, we can NOT mark it as visited the first time it's visited. 
        * So to make DFS work, I have to backtrack after a recursive call to a node's neighbors.
        * This made the algorithm work but the time complexity is hugely large. And I got TLE in the end.
        * I then tried to use cache to speedup the performance. This broke the correctness of the algorithm. As my cache only compares the number of steps, but when the steps are the same, it doesn't compare the path. Also because of this, I can NOT directly re-use the results in the cache, because the number of steps is not optimal, or even if it's optimal, the path is not optimal. It serves no use here. 
    2. After reading the discussion, I now think this problem is a shortest path problem in a weighted edge graph. It's perfect to use Dijkstra algorithm here. 
        * So I implemented the algorithm using priority queue. 
        * However, I didn't get it correct the first time since my state only includes the number of steps, which missed the case for two paths with the same number of steps but we only need the path which is ordered earlier. So I have to add the actual path into the state such that we order first by steps then by the path.

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
* [LC499. The Maze III][LeetCode Link]


[LeetCode Link]: https://leetcode.com/problems/the-maze-iii/