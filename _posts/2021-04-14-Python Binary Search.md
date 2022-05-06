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

0. Once you understand the concept of lower bound and upper bound, you will notice that in general, there are only two ways to code binary search: find lower bound or find upper bound.

1. `bisect_left(a, x, lo=0, hi=len(a))`:
    1. If `x` is already present in `a`, the insertion point will be before (**to the left of**) any existing entries. The return value is suitable for use as the first parameter to `list.insert()` assuming that `a` is already sorted.
    2. The returned insertion point `i` partitions the array `a` into two halves so that `all(val < x for val in a[lo:i])` for the left side and `all(val >= x for val in a[i:hi])` for the right side.
    3. N.B. The array is sorted in increasing order, it won't work with array sorted reversely.
    4. How to implement `bisect_left`?
```
def my_bisect_right(a, x, lo=0, hi=None, *, key=None):
    if lo < 0:
        raise ValueError('lo must be non-negative')
    if hi is None:
        hi = len(a) #N.B. The last possible location is after the full array
                    # Otherwise This doesn't work if there's only 1 element, and x == a[0]
    while lo < hi:
        mid = (lo + hi) // 2
        if a[mid] > x: #Find the lowest index k such that a[k] > x
            hi = mid
        else:
            lo = mid + 1
    return lo

def my_bisect_left(a, x, lo=0, hi=None, *, key=None):
    if lo < 0:
        raise ValueError('lo must be non-negative')
    if hi is None:
        hi = len(a) #N.B. The last possible location is after the full array, 
                    # Otherwise This doesn't work when a=[2,2], and x = 3
    while lo < hi:
        mid = (lo + hi) // 2
        if a[mid] >= x: #Find the lowest index k, such that a[k] >= x
            # If a[mid] == x, the return can be either mid or some index before mid
            # If a[mid] > x, the return can be mid-1 or some earlier position, as hi is one position after the bound, so we can keep hi = mid here.
            hi = mid
        else:
            lo = mid + 1
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
                right = mid  #Think about bisect_right() 
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
            * N.B. If return `left-1`, [we need set the right boundary 1 position right][LC1891. Cutting Ribbons] to the maximum allowable range (if the maximum allowable position might be an answer). 


5. Prove that Binary Search ends with correct position
    1. The formal way is to [prove by induction][Showing binary search correct using strong induction], which you can read up yourself if you are interested. 
    2. Here is a helpful tip to quickly prove the correctness of your binary search algorithm during an interview. We just need to test an input of size 2. Check if it reduces the search space to a single element (which must be the answer) for both of the scenarios above. If not, your algorithm will never terminate.

6. [LC33. Search in Rotated Sorted Array][LC33. Search in Rotated Sorted Array]
    1. The idea is to identify the subarray which is sorted and not rotated in each time
    2. [LC154. Find Minimum in Rotated Sorted Array II][LC154. Find Minimum in Rotated Sorted Array II]
        * We can simplify the conditions by checking the `mid` element with the `high` element

7. [Use binary search to find the maximum of the smallest value or the minimum of the largest value][Use Binary Search to find lower and upper bounds]
    2. Example: [LC410. Split Array Largest Sum][LC410. Split Array Largest Sum]

8. How to set left and right
    1. There are two middle points: `int(lo+(hi-lo)/2)` and `int(lo+(hi-lo+1)/2)`
    2. If we select the first one using `int(lo+(hi-lo)/2)`, we want to make sure to avoid setting `lo = mid` because that might lead to infinite loop.
    3. Similarly, if we select the second one, we want to avoid setting `hi=mid`

9. 在具体的算法问题中，常用到的是「搜索左侧边界」和「搜索右侧边界」这两种场景，很少有让你单独「搜索一个元素」。
    1. 因为算法题一般都让你求最值，比如让你求吃香蕉的「最小速度」，让你求轮船的「最低运载能力」，求最值的过程，必然是搜索一个边界的过程。
    2. 什么问题可以运用二分搜索算法技巧？
        1. 首先，你要从题目中抽象出一个自变量 x，一个关于 x 的函数 f(x)，以及一个目标值 target。
        2. 同时，x, f(x), target 还要满足以下条件：
            * f(x) 必须是在 x 上的单调函数（单调增单调减都可以）。
            * 题目是让你计算满足约束条件 f(x) == target 时的 x 的值。
        3. 来举个具体的例子：给你一个升序排列的有序数组 nums 以及一个目标元素 target，请你计算 target 在数组中的索引位置，如果有多个目标元素，返回最小的索引。
        ```
        // 函数 f(x) 是关于自变量 x 的单调递增函数
        // 入参 nums 是不会改变的，所以可以忽略，不算自变量
        int f(int x, int[] nums) {
            return nums[x];
        }
        ```
        4. 其实这个函数 f 就是在访问数组 nums，因为题目给我们的数组 nums 是升序排列的，所以函数 f(x) 就是在 x 上单调递增的函数。计算元素 target 的最左侧索引？是不是就相当于在问我们「满足 f(x) == target 的 x 的最小值是多少」？








Resources:
* [827. Making A Large Island][LeetCode Link]


[LeetCode Link]: https://leetcode.com/problems/making-a-large-island/
[Powerful Ultimate Binary Search Template]: https://leetcode.com/problems/koko-eating-bananas/discuss/769702/Python-Clear-explanation-Powerful-Ultimate-Binary-Search-Template.-Solved-many-problems.
[lee215 comment in LC1231. Divide Chocolate]: https://leetcode.com/problems/divide-chocolate/discuss/408503/JavaC++Python-Binary-Search/367637
[Showing binary search correct using strong induction]: http://www.cs.cornell.edu/courses/cs211/2006sp/Lectures/L06-Induction/binary_search.html
[LC33. Search in Rotated Sorted Array]: https://leetcode.com/problems/search-in-rotated-sorted-array/
[LC154. Find Minimum in Rotated Sorted Array II]: https://leetcode.com/problems/find-minimum-in-rotated-sorted-array-ii/
[LC410. Split Array Largest Sum]: https://leetcode.com/problems/split-array-largest-sum/
[Use Binary Search to find lower and upper bounds]: https://medium.com/swlh/binary-search-find-upper-and-lower-bound-3f07867d81fb
[LC1891. Cutting Ribbons]: https://leetcode.com/problems/cutting-ribbons/
[我写了首诗，让你闭着眼睛也能写对二分搜索]: https://labuladong.github.io/algo/1/10/
[二分搜索怎么用？我又总结了套路]: https://labuladong.github.io/algo/2/18/28/