---
title: "Numerical Computations"
date: 2021-07-19
categories:
  - blog
tags:
  - algorithm
  - summary
---

1. Overflow
    1. How to check if a computation will overflow?, e.g. `y = x * 10 + r`
        * Assume our maximum/minimum integer is (INT_MAX/INT_MIN): `INT_MAX = 2^31-1 =2147483647` (about `2.1x10^9`), `INT_MIN = -2^31 = -2147483648`
        * Also assume we only allow integer calculations here
        * Then `y > INT_MAX` when `x > INT_MAX//10` or `x==INT_MAX//10 and r > 7`
        * Similarly `y < INT_MIN` when `x < INT_MIN//10` or `x == INT_MIN//10 and r < -8`

2. Problems
    1. [LC7. Reverse Integer][LC7. Reverse Integer]

[LC7. Reverse Integer]: https://leetcode.com/problems/reverse-integer/