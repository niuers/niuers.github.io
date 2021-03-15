---
title: "Recover Binary Search Tree (LC99)"
date: 2021-03-15
categories:
  - blog
tags:
  - algorithm
  - leetcode
  - tree traversal
  - Morris
---

1. Experience:
    1. I know that the inorder traversal of the BST shall give me a sorted array of all nodes. So the pair of mismatched nodes shall appear in wrong places.
        1. First time I didn't think this thoroughly. I thought that the first time we see a number smaller than its previous number, that should be the place where we should do the exchange. However, this doesn't work for the case of `321` where `1` and `3` are swapped.
    2. I then tried some simple cases, e.g. `1`, `12`, `123`, trying to find some pattern from them.
        1. I worked out all the cases for a tree with 3 numbers, and see how can two of the numbers be swapped and how should I fix them.
        2. I realized that I can get the inorder traversal saved into an array, and use the array to find out the two nodes that are out of order. This is because there can be only two numbers that have been swapped. 
        3. So I started to think about how to do the inorder tree traversal. 
            * I first tried recursive method. As I couldn't come up with iterative method immediately.
            * I save the inorder traversal into an array and use it to find out the two nodes that are swapped. I then swap them back.
    3. After successfully implemented the recursive inorder traversal, I started to implement the iterative inorder traversal. I know that I need a stack or double queue, but I wasn't sure which one to use. So I choose double queue here. 
        1. At first, I ran into the problem of only saving immediate children to the queue.
        2. Then I realized that I need to save the left children all the way to the end to have correct inorder traversal. 
        3. That's exactly what I did. After reading the solution, I realized that I only need a stack, not a double queue.
    4. As the problem is asking for `O(1)` space complexity. I thought I can use the minimum/maximum of left/right subtrees to fix the tree. As there are only two nodes, if they exist in a tree, the larger number either swaps with the root, or swaps with some node in left tree.
        1. I started to implement a recursive method based on this. 
        2. It turned out to not exactly correct here. For a BST tree that with two nodes swapped, it's possible that any of the subtree will say that there're nodes out of sync. The problem is we don't know which node shall we swap to because it's possible the other node is out of current subtree and current function has no idea of it.
    5. I gave up and started to read the solutions.
        1. It seems that the `O(1)` space solution is the famous Morris Inorder Traversal.
        2. The main point of Morris method is to set the predecessor's (in terms of inorder sequence) right child to current child. And use that to return to parent node.


2. How did I or Other people get the solution? 


3. Different solutions


4. Mistakes

5. Problem Type
    1. BST
    2. Morris Inorder Traversal
    
6. Similar Problems


7. Template

8. I understand the solution, but HOW do I think to GET there myself?
    1. Where could you improve?
        * I should try to implement Morris method, it doesn't seem to be very hard.
    2. What questions should I ask myself so that I push myself closer to the solution? 
    3. What conclusions did I reach that I dropped some idea for the other? 
    4. How can I reach this conclusion faster ?
    



Resources:
* [99. Recover Binary Search Tree][LeetCode Link]


[LeetCode Link]: https://leetcode.com/problems/recover-binary-search-tree/solution/