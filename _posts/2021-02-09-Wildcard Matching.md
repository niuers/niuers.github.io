---
title: "Wildcard Matching"
date: 2021-02-09
categories:
  - blog
tags:
  - algorithm
  - leetcode
  - dynamic programming
---

1. Experience:
    1. I wrote a brutal force solution first
        * I need call a function recursively to check if the pattern can match the string. Each step I reduce one character in the pattern and possibly one in the string if the current pattern is not `*`
        * If current pattern is `*`, I have to check all possibilies when it can match zero or more characters in the string recursively.
            * After reading the solution, in this case, I can also reduce the string by 1 and keep the pattern the same, i.e. check `s[1:]` vs. `p`
        * This is exponential in time. The submission ended in TLE.
    2. I then added cache for each pair of `(pattern, string)`, I still get TLE
    3. I noticed that if there are multiple `*` connected together, they can be treated as just one `*`, so I did pre-processing to remove any redundant `*` first, then the submission got accepted with 7% rank.
    4. I tried to optimze the algorithm again to skip the recursive call if the character next to `*` in the pattern doesn't equal to the current character in the string. This doesn't improve anything.
    5. After reading the solution and discussion, I realized that one more optimization is to not copy string in each recursive call, but use indices.

    6. I think dynamic programming might help here. So I tried to work out how to use dynamic programming. 
        * I designed a 2-dimensional dynamic table, where `dp[i][j]` is a tuple of bools, e.g. `(True, False)`. The first bool represents whether the pattern `p[:i]` can totally match string `s[:j]`. The second bool says that if there exists any `k for k <=j` such that `p[:i]` can totally match `s[:k]`, then this bool is `True`, otherwise it's `False`.
        * To deal with empty string case, I added extra column in both pattern and string dimensions, so the `dp[0][:]` actually means whether an empty pattern can represent string `s[:j]`, whereas `dp[:][0]` represents whether some pattern `p[:i]` can match an empty string.
        * Once we have the table, it's not that hard to figure out the condition on how to update `dp[i][j]` given previous values.
        * It's clear that in the case current pattern is `*`, if I want to avoid looping through all possible matches, I need the second boolean parameter to record whether it's possible to match using any of previous characters in the string.
        * I had some issues to use a list instead of tuple to represent the pair of booleans. It turns out troublesome to use list in such case as lists are muttable. It's better to use tuple to avoid some tricky bugs.
        * This submission improved to 13%.
        * Noticed that we don't have to save full matrix for the dynamic table, I further optimized the algorithm to just use two rows. This improved the memory usage a lot, and additionally improved the performance to 35%.
        * This has a time complexity of `O(mn)`.


2. How did I get the solution? 
    1. I knew that the brutal force probably will get me TLE.
    2. It looks like that if the brutal force solution is exponential, it's worth to think about dynamic programming. 
    3. As there are two moving parts, one from the pattern, the other from the string, it's better to fix one and think through different cases. The dynamic programming solution turns out to just try to fix both dimensions at each step. This makes the thought process much easier.

3. Different solutions
    1. Turns out backtracking also works too.

4. Mistakes
    1. When make a copy of list, should always use [:] or .copy(), otherwise, it's highly likely the previous list is getting overwritten.
    2. Had many minor bugs, e.g. deal with the first column when I update prevous row with current row, because I always start from 2nd column, so the first column shouldn't change at all.
    3. Forgot to initialize first row, etc.

5. Problem Type
    * A match problem between two things.
    * [String searching algorithm][String_searching] and [KMP algorithm][KMP]

6. Similar Problems

7. Template



Resources:
* [Wildcard Matching][LeetCode Link]

[String_searching]: https://en.wikipedia.org/wiki/String-searching_algorithm
[KMP]: https://en.wikipedia.org/wiki/Knuth%E2%80%93Morris%E2%80%93Pratt_algorithm
[LeetCode Link]: https://leetcode.com/problems/wildcard-matching/