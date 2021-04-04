---
title: "Verify Preorder Sequence in Binary Search Tree (LC255)"
date: 2021-03-30
categories:
  - blog
tags:
  - algorithm
  - leetcode
  - BST
---

1. Experience:
    1. I first saw a clear recursive pattern. Since I know the root for the preorder tree, and can find its right child in `O(n)`, so it sounds straightforward to use recursive method. 
        * The tricky part is how to judge the tree is valid or not. 
        * To achieve this, I have to pass the maximum allowable for the left sub tree and minimum allowable value for the right sub tree when calling the function recursively on sub trees.
        * Then in each call, I use the passed in values to verify that the tree is valid. This takes `O(n)` time complexity because I have to find the maximum and minium each time. 
            * I tried to reduce this calculation to `O(1)` by returning (instead of passing) the maximum/minmum values from the sub-trees. 
        * In each call, I also have to loop through the sub array to find the right child for the current root node. This is also `O(n)`.
        * This however, received TLE.
    2. I then started to think about how to recover the BST using a preorder array.
        * I figured out that we need a stack to save previous nodes (left tree) and pop all left tree nodes out when we see a node has a larger value. 
        * This gives me idea of using stack to check if the tree is valid or not. Instead of just saving the node itself, I save both the maximum, minimum values allowable for the current node's sub trees. 
        * It's not easy to implement the algorithm correctly though. I went through several iterations to check the validity of algorithm.  

2. How did I or Other people get the solution? 
    1. Other people also used stack to solve the problem. They made it simpler by noticing that we don't have to save both max and min allowable values for a sub tree. A lower bound is enough to check if the tree is valid or not. And we don't have to save this lower bound with the stack entries, just update it whenever we pop out stack.

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
* [255. Verify Preorder Sequence in Binary Search Tree][LeetCode Link]


[LeetCode Link]: https://leetcode.com/problems/verify-preorder-sequence-in-binary-search-tree/