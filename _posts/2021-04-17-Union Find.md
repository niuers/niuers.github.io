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
    0. Main interfaces
        * `find(a)`:
        * `union(a,b)`
    1. Use weighted quick-union: The depth of any node in a forest built by weighted quick-union for `N` sites is at most `lg N`. The worst-case order of growth of the cost of `find()`, and `union()` is `log N`. The weighted quick-union algorithm uses at most `c M lg N` array accesses to process `M` connections among `N` sites for a small constant `c`.
    2. **Path Compression**: weighted quick-union with path compression.
        * To implement path compression, we just add another loop to `find()` that sets the `id[]` entry corresponding to each node encountered along the way to link directly to the root.
        * Amortized to almost but not quite constant time for `find()` and `union()`.
    3. Complexity
        * If `K` operations, either Union or Find, are applied to `L` elements, the total run time is `O(Klog*L)`, where `log*` is the iterated logarithm.

2. quick-find vs. quick-union
    1. quick-find: it is a quadratic algorithm for `find()` operation
    2. quick-union: `O(n^2)` in worst case for `union()` operation
    3. weighted quick-union: worst-case logrithmic performance for `find()` and `union()` operations. 
    4. weighted quick-union with path compression: very, very nearly, but not quite `1` (amortized ) cost for `union` and `find`.

3. Template
```

```

[LC323 Number of Connected Components in an Undirected Graph]: https://leetcode.com/problems/number-of-connected-components-in-an-undirected-graph/
[Princeton Tutorial on Union-Find]: https://www.cs.princeton.edu/~wayne/kleinberg-tardos/pdf/UnionFind.pdf
