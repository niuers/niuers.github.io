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

2. Assume our maximum/minimum integer is (INT_MAX/INT_MIN): `INT_MAX = 2^31-1 =2147483647` (about `2.1x10^9`), `INT_MIN = -2^31 = -2147483648`
    1. The key observation to make is that the problems are occurring because there are more negative signed 32-bit integers than there are positive signed 32-bit integers. Each positive signed 32-bit integer has a corresponding negative signed 32-bit integer. However, the same is not true for negative signed 32-bit integers. The smallest one, -2147483648, is alone. It is this number that causes the problems.
    2. One solution is to work with negative, instead of positive, numbers. This is allows us to use the largest possible range of numbers, and it covers all the ones we need.

3. Divide an integer by another integer without using division/multiplication/mod etc.
    1. Repeated Subtraction: `O(n)`
    2. ***Exponential search*** is commonly used for searching sorted spaces of unknown size for the first value that past a particular condition. It it a lot like binary search, having the same time complexity of `O(logn)`. 
    3. Adding powers of 2 of number of divisors needed to sum to division.
    4. Binary Long Division: long division works by find a large multiple of the divisor which fits into the dividend. Then it subtracts this from the dividend and repeats the process.
        1. Long Division in Base-10: One of the problems with using base-10 division for this problem is that in order to perform the algorithm, we'd need to be able to add the necessary 0s onto the end of the divisor
            * Additionally, the current divisor could fit into the current dividend up to 10 times. Again, without multiplication, this is a bit annoying to calculate.
        2. Long Division in Base-2
            * In base-2, division works exactly the same way. However, because there are only two digits (1 and 0), we can simply check if the divisor-padded-with-zeroes is greater than the current dividend, and then if it is, add a 0 digit to the quotient, otherwise add a 1 digit.







4. Problems
    1. [LC7. Reverse Integer][LC7. Reverse Integer]
    2. [LC9. 9. Palindrome Number][LC9. 9. Palindrome Number]

[LC7. Reverse Integer]: https://leetcode.com/problems/reverse-integer/
[LC9. 9. Palindrome Number]: https://leetcode.com/problems/palindrome-number/