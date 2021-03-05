---
title: "Minimum Height Trees (LC310)"
date: 2021-03-05
categories:
  - blog
tags:
  - algorithm
  - leetcode
  - graph
---

1. Experience:
    1. I wrote the brutal force solution. Loop on each node, find the maximum height with each node as root, and compare the heights to get the minimum height. 
        * To find the height of each tree, I recursively call a DFS function until I exhaust all the nodes. This will take `O(V+E)`.
        * The total time complexity will be `O(V(V+E))`.
    2. I then tried to find a better algorithm. 
        * I noticed that the nodes with only 1 connection couldn't be the root of a minimum height tree (unless there're only two nodes). 
        * I also noticed that the nodes that give us minimum trees are in the center of a path.
        * I couldn't convert the above two observations into a solution. 
    3. I couldn't find a better solution so I had to look into the solution. It turns out that my observations are all related to the better solution. 
        * I should continuously apply the observation that leaves can't be the centroids to find the trees with minimum height.
        * Another solution is to find the maximum distance among the nodes, then the middle point(s) are the answer.

2. How did I or Other people get the solution? 


3. Different solutions




4. Mistakes

5. Problem Type
    * Graph
    * Topological Sort
    * BFS

6. Similar Problems
  1. 


7. Template



Resources:
* [310. Minimum Height Tree][LeetCode Link]


[LeetCode Link]: https://leetcode.com/problems/minimum-height-trees/