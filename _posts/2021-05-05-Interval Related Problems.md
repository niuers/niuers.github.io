---
title: "Interval Related Problems"
date: 2021-05-08
categories:
  - blog
tags:
  - algorithm
  - interval
  - summary
---

1. Two intervals `[s1, e1)` and `[s2, e2)` do not intersect if and only if one of them starts after the other one ends: either `e1 <= s2` OR `e2 <= s1`. By De Morgan's laws, this means the events intersect when `s1 < e2` AND `s2 < e1`. From [LC729 solution][LC729. My Calendar I].

2. Merge an array of intervals into non-overlap intervals
    1. We can sort the intervals first and merge from left to right: `O(nlogn)`
    2. We can create a tree of intervals such that adding a new interval takes `O(logn)`. For the treeNode, we use extra fields: `start_loc, end_loc, middle_loc`. Any interval that is on the left of current node's `middle_loc` is inserted to its left child.    
    3. Problems
        * [LC56. Merge Intervals][LC56. Merge Intervals]





[LC1423. Maximum Points You Can Obtain from Cards]: https://leetcode.com/problems/maximum-points-you-can-obtain-from-cards/solution/
[LC56. Merge Intervals]: https://leetcode.com/problems/merge-intervals/