---
title: "Interval Related Problems"
date: 2021-05-05
categories:
  - blog
tags:
  - algorithm
  - summary
---

1. Two intervals `[s1, e1)` and `[s2, e2)` do not conflict if and only if one of them starts after the other one ends: either `e1 <= s2` OR `e2 <= s1`. By De Morgan's laws, this means the events conflict when `s1 < e2` AND `s2 < e1`. From [LC729 solution][LC729. My Calendar I].
2. How to compute the time complexity of backtracking algorithm?





[LC729. My Calendar I]: https://leetcode.com/problems/my-calendar-i/