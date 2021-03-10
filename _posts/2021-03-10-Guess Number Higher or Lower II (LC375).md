---
title: "Guess Number Higher or Lower II (LC375)"
date: 2021-03-10
categories:
  - blog
tags:
  - algorithm
  - leetcode
  - dynamic programming
---

1. Experience:
    1. I didn't start with brutal force solution since I didn't spend much time thinking about how to make it work. I thought I can work out a dynamic programming solution.
    2. For a given `n`, I understand that I need to go through from 1 to `n`, for each of these numbers, it splits the numbers into left and right halfs. The minimum amount for `n` is the minimum of the amounts when spliting on `1, 2, ..., n`. 
    3. On a specific split point `i`, I want to find out how to reuse previously computed results. Assuming we have a function `f(n)` that computes the minimum amount of money. It's simple on left side since we just need to reuse `f(i)`. 
    4. However, the right half is much harder to figure out. As we have numbers `i+1, i+2, ..., n`. I thought I can use `i+ (1,2,...,n-i)` to represent them, such that I can reuse `f(n-i)` by just adding `i` to `f(n-i)`. If this works, I can just choose the maximum of `f(i)` and `i+f(n-i)` to get the amount when we split at `i`. Doing this for `1,2,..,n` and pick the minimum of the amounts, I'll get the answer for `f(n)`. 
        * It didn't work though, since for each `f(i)` tree, we may have to go through different depths to achieve the amount. So `i+f(n-i)` only works if the tree `f(n-i)` has depth `1`. For example, I can use `4+f(3)` to compute the amount for `5,6,7` as `f(3) = 2` and `f(5,6,7) = 6`. This is because the tree `f(3)` has only 1 level.
        * If we want to compute `f(4,5,6,7)`, then it doesn't equal to `3+f(4)` since there are two levels, we need to use `3*2+f(4)`.
    5. Because of the above level issue, I then tried to save the levels used in calcultion so I can put the level into the formula. 
        * It's very tricky though. Because there are cases that for smaller numbers, we obtain its maximum amount using right tree (so the level will be the depth of right tree), but when we reuse it to compute the amount for a larger tree, I found that the amount is achieved on the left of this tree. This says that the information of depth is not enough. I need to save the depth information for both left and right sub-trees.
        * That's exactly what I did. Still, it ran into errors for some test cases, where the number is too large to debug.
        * I think it's possible that when I choose which depth information to save, it works for some cases, but not for all cases. This is a dead end here.
    6. I checked the solutions, and it totally makes sense to use a two-dimensional dynamic table, where we first compute the answers with smaller length then re-use them in later computations.
        * Compare this with my solution, it solves my problem perfectly as I couldn't figure out how to compute the right half's amount by reusing previous results. That's because I only considered to compute the amount from `1 to n`, instead the solution considers the calculations of amounts from `i to j` for any `i` and `j`.

2. How did I or Other people get the solution? 


3. Different solutions




4. Mistakes

5. Problem Type

6. Similar Problems
  1. 


7. Template



Resources:
* [375. Guess Number Higher or Lower II][LeetCode Link]


[LeetCode Link]: https://leetcode.com/problems/guess-number-higher-or-lower-ii/