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

3. Check if an interval can be assigned with previous intervals into the same room
    1. Min-heap:
        * Sort the intervals first
        * Then use a min-heap to check the interval with the smallest ending time
    2. Chronological Ordering
        * We treat the start and end times individually
        * When we encounter an ending event, that means that some meeting that started earlier has ended now. We are not really concerned with which meeting has ended. All we need is that some meeting ended thus making a room available.
        * We use two pointers for start and end times separately, and compare them to see if a room is available nor not.




[LC1423. Maximum Points You Can Obtain from Cards]: https://leetcode.com/problems/maximum-points-you-can-obtain-from-cards/solution/
[LC56. Merge Intervals]: https://leetcode.com/problems/merge-intervals/