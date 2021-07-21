---
title: "Dealing with Corner Cases"
date: 2021-07-20
categories:
  - blog
tags:
  - algorithm
  - summary
---

1. Check if the index is out of bound when accessing array element
    1. `arr[0]`: check if the array is empty before using this element
    2. `arr[i]`: check if `0 <= i < len(arr)`
    3. Related Problems
        * [LC8. String to Integer (atoi)][LC8. String to Integer (atoi)]

2. Check each branch in your conditional statements, make sure they are correct, and if the final result is obtained by combining several steps together, make sure the final one is correct.

[LC8. String to Integer (atoi)]: https://leetcode.com/problems/string-to-integer-atoi/
