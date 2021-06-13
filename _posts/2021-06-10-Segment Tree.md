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

1. Segment Tree:
    1. Solve range query problems: what's the minimum/maximum/sum in a range?
        * Alternative methods:
            * Use linear scan `O(n)` per scan, and `O(mn)` for `m` queries
            * Use table to store the range results, need `O(n^2)` to generate the table, `O(1)` query time.
        * Segment Tree Complexities:
            * `O(n)` to build a segment tree
            * `O(n)` space
            * `O(logn)` to query
    2. When query we can consider 3 cases:
        * partial overlap: need go left and right children
        * total overlap: Current node's range is totally covered by the query range
        * no overlap: 
    3. Methods
        * We can use recursion to build a segment Tree
        * Iterative method works as well.

2. [Lazy Propagation in Segment Tree][Lazy Propagation Segment Tree]
    1. It's an optimization when there are lots of updates in the segment tree. It minimizes the number of operations on the nodes for the segment tree.
    2. Use a lazy tree: 

3. Different solutions


4. Mistakes

5. Problem Type
    
6. Similar Problems

7. Template

8. I understand the solution, but HOW do I think to GET there myself?
    
[Lazy Propagation Segment Tree]: https://www.youtube.com/watch?v=xuoQdt5pHj0&t=444s


