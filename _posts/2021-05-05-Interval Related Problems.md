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

1. Two intervals `[s1, e1)` and `[s2, e2)` do not conflict if and only if one of them starts after the other one ends: either `e1 <= s2` OR `e2 <= s1`. By De Morgan's laws, this means the events conflict when `s1 < e2` AND `s2 < e1`. From [LC729 solution][LC729. My Calendar I].






[LC1423. Maximum Points You Can Obtain from Cards]: https://leetcode.com/problems/maximum-points-you-can-obtain-from-cards/solution/