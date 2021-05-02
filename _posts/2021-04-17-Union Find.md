---
title: "Union Find"
date: 2021-04-14
categories:
  - blog
tags:
  - algorithm
  - leetcode
  - union-find
  - summary
---

1. Improvements to quick-union algorithm
    1. Use weighted quick-union: The depth of any node in a forest built by weighted quick-union for `N` sites is at most `lg N`. The worst-case order of growth of the cost of find(), and union() is `log N`. The weighted quick-union algorithm uses at most `c M lg N` array accesses to process `M` connections among `N` sites for a small constant `c`.
    2. Path Compression: weighted quick-union with path compression.
        * To implement path compression, we just add another loop to find() that sets the id[] entry corresponding to each node encountered along the way to link directly to the root.
        * Amortized to almost but not quite constant time for find(), union().

