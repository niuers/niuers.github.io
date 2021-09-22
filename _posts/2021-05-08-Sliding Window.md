---
title: "Sliding Window"
date: 2021-05-10
categories:
  - blog
tags:
  - algorithm
  - sliding window
  - summary
---

1. With the two pointers, we can consider save following information along with:
  1. The right most position
  2. The count of characters
  3. Problems
      * [LC159. Longest Substring with At Most Two Distinct Characters][LC159. Longest Substring with At Most Two Distinct Characters]
      * [LC3. Longest Substring Without Repeating Characters][LC3. Longest Substring Without Repeating Characters]

2. [General summary of what kind of problem can/cannot solved by Two Pointers][General summary of what kind of problem can/ cannot solved by Two Pointers]
  1. A problem can be solved by two pointers when two pointers come into place to help us reduce the total cases we need to consider, such that the corresponding time complexity will reduce too.
  2. We can't solve a problem by two pointers if:
    * When a narrower scope of the sliding window (with maximum possible size) is valid, but a wider scope of that narrower scope can still be valid with the sizes between as invalid.



[LC159. Longest Substring with At Most Two Distinct Characters]: https://leetcode.com/problems/longest-substring-with-at-most-two-distinct-characters/
[General summary of what kind of problem can/ cannot solved by Two Pointers]: https://leetcode.com/problems/subarray-sum-equals-k/discuss/301242/General-summary-of-what-kind-of-problem-can-cannot-solved-by-Two-Pointers
[LC3. Longest Substring Without Repeating Characters]: https://leetcode.com/problems/longest-substring-without-repeating-characters/
[LC560. Subarray Sum Equals K]: https://leetcode.com/problems/subarray-sum-equals-k/
