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
    2. Given an integer, it can overflow (exceeding `INT_MAX`) if we reverse its digits, e.g. `123` --> `321`. We can just reverse half of the number to avoid overflow. To check if we have arrived at the half, we compare the reversed integer with the original integer (which has been reduced by dividing by 10). We stop when the former is greater than the latter.

2. Problems
    1. [LC7. Reverse Integer][LC7. Reverse Integer]
    2. [LC9. 9. Palindrome Number][LC9. 9. Palindrome Number]

[LC7. Reverse Integer]: https://leetcode.com/problems/reverse-integer/
[LC9. 9. Palindrome Number]: https://leetcode.com/problems/palindrome-number/