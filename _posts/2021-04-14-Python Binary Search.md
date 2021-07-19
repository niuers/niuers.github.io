---
title: "Python Binary Search"
date: 2021-04-14
categories:
  - blog
tags:
  - algorithm
  - leetcode
  - binary search
  - summary
---

1. `bisect_left(a, x, lo=0, hi=len(a))`:
    1. If `x` is already present in `a`, the insertion point will be before (**to the left of**) any existing entries. The return value is suitable for use as the first parameter to `list.insert()` assuming that `a` is already sorted.
    2. The returned insertion point `i` partitions the array `a` into two halves so that `all(val < x for val in a[lo:i])` for the left side and `all(val >= x for val in a[i:hi])` for the right side.



2. `bisect_right(a, x, lo=0, hi=len(a))` and `bisect(a, x, lo=0, hi=len(a))`:
    1. It returns an insertion point which comes after (to the right of) any existing entries of `x` in `a`.


3. [lee215 quote][lee215 comment in LC1231. Divide Chocolate]Quick tip: if you have `left = mid`, use `left + right + 1`. It's possible to use left <= right. But if you follow my all posts, I almost always use left < right.



4. Binary Search Template
    1. [Powerful Ultimate Binary Search Template in Python][Powerful Ultimate Binary Search Template]




Resources:
* [827. Making A Large Island][LeetCode Link]


[LeetCode Link]: https://leetcode.com/problems/making-a-large-island/
[Powerful Ultimate Binary Search Template]: https://leetcode.com/problems/koko-eating-bananas/discuss/769702/Python-Clear-explanation-Powerful-Ultimate-Binary-Search-Template.-Solved-many-problems.
[lee215 comment in LC1231. Divide Chocolate]: https://leetcode.com/problems/divide-chocolate/discuss/408503/JavaC++Python-Binary-Search/367637