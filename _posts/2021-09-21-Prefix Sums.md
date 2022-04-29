---
title: "Prefix Sums"
date: 2021-09-21
categories:
  - blog
tags:
  - algorithm
  - summary
---

1. [Prefix Sums][LC437. Path Sum III]
  1. It could be defined for 1D arrays (sum the current value with all the previous integers),
  2. for 2D arrays (sum of the current value with the integers above or on the left)
  3. for the binary trees (sum the values of the current node  and all parent nodes),
  4. 前缀和主要适用的场景是原始数组不会被修改的情况下，频繁查询某个区间的累加和。

2. [差分数组][小而美的算法技巧：差分数组]
  1. 差分数组的主要适用场景是频繁对原始数组的某个区间的元素进行增减。这样构造差分数组 diff，(diff[i] 就是 nums[i] 和 nums[i-1] 之差)就可以快速进行区间增减的操作

4. Problems
    1. [LC921. Minimum Add to Make Parentheses Valid][LC921. Minimum Add to Make Parentheses Valid]
    
[LC437. Path Sum III]: https://leetcode.com/problems/path-sum-iii/
[小而美的算法技巧：差分数组]: https://labuladong.github.io/algo/2/18/22/



