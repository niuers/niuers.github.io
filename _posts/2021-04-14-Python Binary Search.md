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
    3. N.B. The array is sorted in increasing order, it won't work with array sorted reversely.
    4. How to implement `bisect_left`?
```
def bisect_right(a, x, lo=0, hi=None, *, key=None):
    if lo < 0:
        raise ValueError('lo must be non-negative')
    if hi is None:
        hi = len(a)
    while lo < hi:
        mid = (lo + hi) // 2
        if x < a[mid]:
            hi = mid
        else:
            lo = mid + 1
    return lo

def bisect_left(a, x, lo=0, hi=None, *, key=None):
    if lo < 0:
        raise ValueError('lo must be non-negative')
    if hi is None:
        hi = len(a)
    while lo < hi:
        mid = (lo + hi) // 2
        if a[mid] < x:
            lo = mid + 1
        else:
            # If a[mid] == x, the return can be either mid or some index before mid
            # If a[mid] > x, the return can be mid-1 or some earlier position, as hi is one position after the bound, so we can keep hi = mid here.
            hi = mid 
    return lo
```


2. `bisect_right(a, x, lo=0, hi=len(a))` and `bisect(a, x, lo=0, hi=len(a))`:
    1. It returns an insertion point which comes after (to the right of) any existing entries of `x` in `a`.


3. [lee215 quote][lee215 comment in LC1231. Divide Chocolate]Quick tip: if you have `left = mid`, use `left + right + 1`. It's possible to use left <= right. But if you follow my all posts, I almost always use left < right.


4. Binary Search Template
    1. [Powerful Ultimate Binary Search Template in Python][Powerful Ultimate Binary Search Template]
        * Suppose we have a search space. It could be an array, a range, etc. Usually it's sorted in ascending order. For most tasks, we can transform the requirement into the following generalized form:
        * **Minimize k , s.t. condition(k) is True**
        * The following code is the most generalized binary search template:
    ```
    def binary_search(array) -> int:
        def condition(value) -> bool:
            pass

        left, right = min(search_space), max(search_space) # could be [0, n], [1, n] etc. Depends on problem
        while left < right:
            mid = left + (right - left) // 2
            if condition(mid):
                right = mid
            else:
                left = mid + 1
        return left
    ```        
    2. What's really nice of this template is that, for most of the binary search problems, we only need to modify three parts after copy-pasting this template, and never need to worry about corner cases and bugs in code any more:
        * Design the condition function. This is the most difficult and most beautiful part. Needs lots of practice.
        * Correctly initialize the boundary variables left and right to specify search space. Only one rule: set up the boundary to include all possible elements;
            * For example, if you want to implement `bisect_left`, the condition can be "greater and equal to target value", then the minimal of such index `k` is the return value needed. For a given array, the valid return ranges from `0` to `len(a)`, so to make sure the return value covers this range, we should initialize `left=0, right=len(a)`
            * If you want to implement `bisect_right`, the condition can be "greater than the target value", then the minimal of such index `k` is the return value needed. For a given array, the valid return ranges from `0` to `len(a)`, so to make sure the return value covers this range, we should initialize `left=0, right=len(a)`
         * Decide return value. Is it return `left` or return `left - 1`? **Remember this: after exiting the while loop, left is the minimal k​ satisfying the condition function**;
            * N.B. If return `left-1`, we need set the right boundary 1 position right to the maximum allowable range. 


5. Prove that Binary Search ends with correct position
    1. The formal way is to [prove by induction][Showing binary search correct using strong induction], which you can read up yourself if you are interested. 
    2. Here is a helpful tip to quickly prove the correctness of your binary search algorithm during an interview. We just need to test an input of size 2. Check if it reduces the search space to a single element (which must be the answer) for both of the scenarios above. If not, your algorithm will never terminate.


Resources:
* [827. Making A Large Island][LeetCode Link]


[LeetCode Link]: https://leetcode.com/problems/making-a-large-island/
[Powerful Ultimate Binary Search Template]: https://leetcode.com/problems/koko-eating-bananas/discuss/769702/Python-Clear-explanation-Powerful-Ultimate-Binary-Search-Template.-Solved-many-problems.
[lee215 comment in LC1231. Divide Chocolate]: https://leetcode.com/problems/divide-chocolate/discuss/408503/JavaC++Python-Binary-Search/367637
[Showing binary search correct using strong induction]: http://www.cs.cornell.edu/courses/cs211/2006sp/Lectures/L06-Induction/binary_search.html