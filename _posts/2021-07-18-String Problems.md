---
title: "String Problems"
date: 2021-07-18
categories:
  - blog
tags:
  - algorithm
  - string
  - summary
---

1. Palindromes
    1. Check if a string is palindrome
        * Reverse the string and compare with the original string
        * Use two pointers from left and right, and compare each character along the way
    2. Find the longest palindromic substrings
        1. dynamic programming: `O(n^2)`
        2. Expand from center: for each position, expand for the cases of even/odd number of characters and find the longest palindrome. This is much faster than the dynamic programming solution even it's still `O(n^2)`
    7. Problems
        * [LC5. Longest Palindromic Substring][LC5. Longest Palindromic Substring]

2. ZigZag Conversion
    1. Use a combination of current row number and direction to record the string on each row
    2. Problems
        * [LC6. ZigZag Conversion][LC6. ZigZag Conversion]

[LC5. Longest Palindromic Substring]: https://leetcode.com/problems/longest-palindromic-substring/
[LC6. ZigZag Conversion]: https://leetcode.com/problems/zigzag-conversion/