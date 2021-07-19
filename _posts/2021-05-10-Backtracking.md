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
    * We know that the trace of the backtrack would form a n-ary tree. Therefore, the upper bound of the operations would be the total number of nodes in a full-blossom n-ary tree.
        * For example, In problem [425. Word Squares][LC425 Word Squares], at any node of the trace, at maximum it could have 26 branches (i.e. 26 alphabet letters). Therefore, the maximum number of nodes in a 26-ary tree would be approximately `26^L`, where `L` is the height of the tree.






[LC729. My Calendar I]: https://leetcode.com/problems/my-calendar-i/
[LC425 Word Squares]: https://leetcode.com/problems/word-squares/