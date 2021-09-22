---
title: "Segment Tree"
date: 2021-06-10
categories:
  - blog
tags:
  - algorithm
  - leetcode
  - Segment Tree
  - summary
---

1. [Segment Tree][Efficient and easy segment trees]: 
    1. Solve range query problems: what's the minimum/maximum/[sum][LC307. Range Sum Query - Mutable] in a range?
        * Alternative methods:
            * Use linear scan `O(n)` per scan, and `O(mn)` for `m` queries
            * Use table to store the range results, need `O(n^2)` to generate the table, `O(1)` query time.
        * Segment Tree Complexities:
            * `O(n)` to build a segment tree
            * `O(n)` space
            * `O(logn)` to query/update a node
        * Notice that the height of a segment tree for an interval with `N` elements is `[logN] + 1`.
    2. When query we can consider 3 cases:
        * partial overlap: need go left and right children
        * total overlap: Current node's range is totally covered by the query range
        * no overlap: 
    3. Methods
        * We can use recursion to build a segment Tree
        * Iterative method works as well.
    4. Implementation
        * Use an array:
            * The total number of elements is `2*n-1` for a full binary tree, the nodes are from `1,..., 2n-1`, where the node at `0` is not used, and nodes at `n, n+1, ..., 2n-1` are from the original array.
            * If the element at index `i` is not a leaf, its left and right children are stored at index `2i` and `2i+1` respectively. The parent of index `i` is at `int(i/2)`
            * If `L`, the interval's left border is odd , then `L` is the right child of its parent. Its parent is `(L-1)/2`. If `L` is even, then its left child, and its parent is `L/2`
            * If `i<j` the left and right children will hold the information for the intervals `[i, (i+j)/2]` and `[(i+j)/2+1, j]`
            * Segmented tree for array with nn elements has `n` leaves (the array elements itself). The number of nodes in each level is half the number in the level below. So there are approximately `2n` nodes in a segment tree
            * We can build the tree bottom-up, move from right to left of the array. `O(n)`
        * Use a tree:

2. [Lazy Propagation in Segment Tree][Lazy Propagation Segment Tree]
    1. It's an optimization when there are lots of updates in the segment tree. It minimizes the number of operations on the nodes for the segment tree.
    2. [Use a lazy tree][Lazy Propagation]: 



   
[Lazy Propagation Segment Tree]: https://www.youtube.com/watch?v=xuoQdt5pHj0&t=444s
[LC307. Range Sum Query - Mutable]: https://leetcode.com/problems/range-sum-query-mutable/
[Efficient and easy segment trees]: https://codeforces.com/blog/entry/18051
[Lazy Propagation]: https://leetcode.com/articles/a-recursive-approach-to-segment-trees-range-sum-queries-lazy-propagation/

