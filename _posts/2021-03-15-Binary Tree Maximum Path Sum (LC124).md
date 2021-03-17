---
title: "Binary Tree Maximum Path Sum (LC124)"
date: 2021-03-15
categories:
  - blog
tags:
  - algorithm
  - leetcode
  - tree
---

1. Experience:
    1. The first question I asked is how to find a path in a tree? A path can start at any node in the tree, how do I specify a path by going through all nodes? 
    2. I decided to try some simple cases first. It's easy to see the answers for 1,2,3 nodes in a tree.
    3. I then thought about a path that "passes through" a node? 
        * Can I define such a path clearly? Seems not.
        * How about a path that "ending with" a node? Sounds reasonable here.
        * Should I say a path that "ending with non leaf node"? Are we always having a path ending with leaf nodes? This seems wrong. So the definition of a path that "ending with a node" sounds reasonable.
    4. I then thought that recursive method might be a good solution here.
        * There no clear structure that says I can do iterative on the nodes.
        * For a given root, the path with maximum sum is among following cases:
            * In the left sub-tree
            * In the right sub-tree
            * Is a path that passing current root
        * This sounds promising. I started to work out examples that can utilize the above classification.
        * In the case that leaf nodes are negative, I should consider the case that the root itself can be the path with maximum sum.
    5. I started to implement the solution according to above thinking process.
        * The recursive function will return the maximum sum ending with root from left/right subtrees, and the maximum sum path passing through the current root.
    6. I ran into some errors:
        * Case `[-3]`: When a root is `None`, I should return `0,0,-math.inf` instead of `0,0,0` such that `0` won't be the maximum sum in this case.
        * Case `[2, -6, -6, -6]`: My implementation missed the case where `2` is the maximum sum path.
        * It turns out that I should incorporate the root itself as a special case when I look for the paths with maximum path ending with root from left/right subtrees.


2. How did I or Other people get the solution? 


3. Different solutions
    1. The solution is much simpler to implement when they assume the recursive function returns the maximum gains from current node.

4. Mistakes or Improvements
    1. I used cache to try to save the time cost, but turns out we don't need to reuse a node once we have obtained its maximum paths. so the cache is useless.
    2. I don't have to retrun the maximum sum we have obtained so far in the function. Just update it with a global variable.

5. Problem Type
    
6. Similar Problems


7. Template

8. I understand the solution, but HOW do I think to GET there myself?
    1. Where could you improve?
    2. What questions should I ask myself so that I push myself closer to the solution? 
    3. What conclusions did I reach that I dropped some idea for the other? 
    4. How can I reach this conclusion faster ?
    



Resources:
* [124. Binary Tree Maximum Path Sum][LeetCode Link]


[LeetCode Link]: https://leetcode.com/problems/binary-tree-maximum-path-sum/