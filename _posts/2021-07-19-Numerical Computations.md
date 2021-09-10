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
        * Assume our maximum/minimum integer is (INT_MAX/INT_MIN): `INT_MAX = 2^31-1 =2147483647` (about `2x10^9`), `INT_MIN = -2^31 = -2147483648`
        * Also assume we only allow integer calculations here
        * Then `y > INT_MAX` when `x > INT_MAX//10` or `x==INT_MAX//10 and r > 7`
        * Similarly `y < INT_MIN` when `x < INT_MIN//10` or `x == INT_MIN//10 and r < -8`
    2. Given an integer, it can overflow (exceeding `INT_MAX`) if we reverse its digits, e.g. `123` --> `321`. We can just reverse half of the number to avoid overflow. To check if we have arrived at the half, we compare the reversed integer with the original integer (which has been reduced by dividing by 10). We stop when the former is greater than the latter.
    3. `1 000 000 007` and `1 000 000 009` are known large prime number that you can use to get the benefits of a prime modulo, and they don't let your values overflow since `int` is usually `<= 2 * 10 ^ 9`.



2. Assume our maximum/minimum integer is (INT_MAX/INT_MIN): `INT_MAX = 2^31-1 =2147483647` (about `2.1x10^9`), `INT_MIN = -2^31 = -2147483648`
    1. The key observation to make is that the problems are occurring because there are more negative signed 32-bit integers than there are positive signed 32-bit integers. Each positive signed 32-bit integer has a corresponding negative signed 32-bit integer. However, the same is not true for negative signed 32-bit integers. The smallest one, `-2147483648`, is alone. It is this number that causes the problems.
        * One thing to note is that we often want to convert a negative integer to a positive one, this is no problem in Python, but in other programming languages, this conversion will overflow for the smallest integer, i.e. `-2147483648`.
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


4. Multiply two integers represented by string
    1. Use the normal elementary school multiplication method
    2. Find the value at digit position of 1, 10, 100, ..., separately


5. Computer the power of a number, e.g. `pow(x, n)`
    1. Use recursion method
    2. Represent the power `n` as binary number and `n` is thus sum of the corresponding powers of `2`. Then we can use iterative method to compute the power. It stops when the power is 0 (we divide it by 2 each time).
    3. Problems
        * [LC50. Pow(x, n)][LC50. Pow(x, n)]

6. Interger division
    1. `-121//7= -18`, `int(-121/7)=-17`. The latter is truncated toward `0`

7. The cost of integer multiplication
    1. Generally multiplications are on numbers within a fixed bit-size (e.g. 32 bit or 64 bit ints), we treat them as `O(1)` operations. However, as the size of the numbers to be multiplied grow, we can no longer assume this (as Python can represent arbitrary large integers, it's clear that the integers in Python won't have fixed size when they become large).
    2. A popular way people multiply two large numbers, that you probably learned in school, [has a cost][Complexity of arithmetic operations] of `O((logx)(logy))`.
        * If `a` and `b` are, for example, `float`s, then the complexity of `a*b` or `a+b` is  `O(1)`. That's because, for numbers that have a set number of digits, operations like addition and multiplication are performed by the CPU. To simplify a little bit, if the CPU's clock speed is 2Ghz, that means it can perform 2 billion elementary operations like addition or multiplication per second.
        * However, for ints, the story is more complicated, since they do not have a set number of digits, and can be arbitrarily large.
        * Roughly speaking, `a+b` requires as many additions as there are digits in  `max(a,b)`, which is `O(max(log a,log b))`
        * The complexity of long multiplication is  `O(loga×logb)`
    3. Problems
        * [LC172. Factorial Trailing Zeroes][LC172. Factorial Trailing Zeroes]    

8. Check how many 5s are in the factorial of `n`, i.e. `n!`
    1. For each number, check how many 5s are in a number by counting how many times a number can be divided by 5. `O(n)`. The vast majority of numbers checked only contain a single factor of 5. It can be proven that the total number of fives is less than `(2n)/5` 
        ```
        res = 0
        while n > 0 and n % 5 == 0:
          res += 1
          n = n//5
        ```
    2. Count how many times `n` can be divided by 5, 25, 125, ..., and add them together. `O(logn)`
        * N.B. The extra 5 in 25 is counted by previous 5, similarly for 125.
        ```
        res = 0        
        while n > 0:            
            n = n//5
            res += n
        ```

    3. Problems
        * [LC172. Factorial Trailing Zeroes][LC172. Factorial Trailing Zeroes]    

9. Find all prime numbers less than `n`
    1. It's `O(sqrt(n))` complexity to check if a number is prime
    2. Sieve of Eratosthenes `O(\sqrt(n)loglogn)`: 
        * We can start with the smallest prime number, 2, and mark all of its multiples up to "n" as non-primes. Then we repeat the same process for the next available number in the array that is not marked as composite and so on.
        * The outer loop will start at 2 and go up to `sqrt(n)`, This is because by that point we will have considered all of the possible multiples of all the prime numbers below `n`. `O(sqrt(n))`
        * For the inner loop, We will invariantly pick the next available prime number (a number/index not yet marked in the array as a composite) before entering the inner loop. Say the index we picked from the outer loop is `i`, then the inner loop will start at `i*i` and increase by increments of `i` until it surpasses `n`. In short, we iterate over every multiple of `i` between `i` and `n`. 
        * N.B. the prime numbers smaller than `i` would have already covered the multiples smaller than `i*i`.

10. Using `e` will set the number to float. For example, `1e+9` is a float number not an integer in python. You need use `1000000000` instead.

11. [Check if a number if power of 3][LC326. Power of Three]
    1. As 3 is prime number, if we use 32-bit to represent integers, the maximum power of 3 is `3**19`, so any number that divides `3**19` is a power of 3. i.e. `3**19 % n == 0`
    2. You can also check if `log(n, 3)` is an integer. however, you need pay attention to floating point number computations, i.e. use tolerance when do comparison. 
        * e.g. `log(243,3)` could be `5.0000001` or `4.9999999`, so we want to use a small number, e.g. `epsilon =1.0e-12` to account for this, i.e. ` (log(n,3) + epsilon) % 1 < 2*epsilon`, the `2` on the right is because, in the case of `5.0000001`, the left side will be `0.0000001 + epsilon`
        * It's not so easy to choose the `epsilon` though. It can't be too small or too large. 
            * If it's too small and `log(n,3)` is a nummber smaller than the cloest integer, adding to too small number won't make it pass the integer, thus the `%` operation will result in a number closer to 1.
            * If it's too large and `log(n,3)` is a number larger than the cloest integer, the inequality can be true for number that's not a power of 3.

12. Check if a number is perfect square
    1. `num` is a perfect square if `x * x == num`
    2. Use binary search to find the smallest number that satisfying `v*v >= num`
        * For `num>2` the square root `a` is always less than `num/2` and greater than `1`
    3. Use Newton's method: you can use graph (tangent) to help derive the equation: `O(logn)`. N.B. Newton's method converges quadratically.

13. Digital Root
    1. `dr(0) = 0, dr(9k) = 9, dr(n) = n mod 9`
    2. Remember that "The original number is divisible by 9 if and only if the sum of its digits is divisible by 9", One could expand each power of ten into `9k + 1`

14. [Factor computations][LC254. Factor Combinations]
    1. To enumerate all factor combinations, we only need to try out the numbers from `2` to `sqrt(n)`, which can be tested by `i*i < n`.
    2. We need avoid duplicates, e.g. if `n=12`, `[2,2,3] and [3,2,2]` are duplicates if we start from `2` and `3` separately. 
        * to avoid this, if we start with a factor `i`, then to get all the factors of `n/i`, we should start from `i`, not from `2`.

15. Greatest Common Divisor (GCD)
    1. [The Euclidean Algorithm][The Euclidean Algorithm]
        * GCD(A, B) = GCD(A-B, B) = GCD(A-kB, B) = GCD(A%B, B) = GCD(B, A%B)
        ```
        def gcd(a, b):            
            while b > 0:
                a, b = b, a%b
            return a
        ```
    2.  [Bezout's identity][Bezout's identity]
        * We can always find `a` and `b` to satisfy `ax + bx = d` where `d = gcd(x, y)`

16. Problems
    1. [LC7. Reverse Integer][LC7. Reverse Integer]
    2. [LC9. 9. Palindrome Number][LC9. 9. Palindrome Number]
    3. [LC326. Power of Three][LC326. Power of Three]
    4. [LC367. Valid Perfect Square][LC367. Valid Perfect Square]
    5. [LC258. Add Digits][LC258. Add Digits]



[LC7. Reverse Integer]: https://leetcode.com/problems/reverse-integer/
[LC9. 9. Palindrome Number]: https://leetcode.com/problems/palindrome-number/
[LC50. Pow(x, n)]: https://leetcode.com/problems/powx-n/
[LC172. Factorial Trailing Zeroes]: https://leetcode.com/problems/factorial-trailing-zeroes/
[Complexity of arithmetic operations]: https://www.cs.toronto.edu/~guerzhoy/180/lectures/W11/lec1/ComplArithm.html
[LC326. Power of Three]: https://leetcode.com/problems/power-of-three/
[LC367. Valid Perfect Square]: https://leetcode.com/problems/valid-perfect-square/
[LC258. Add Digits]: https://leetcode.com/problems/add-digits/
[LC254. Factor Combinations]: https://leetcode.com/problems/factor-combinations/
[The Euclidean Algorithm]: https://www.khanacademy.org/computing/computer-science/cryptography/modarithmetic/a/the-euclidean-algorithm
[Bezout's identity]: https://en.wikipedia.org/wiki/B%C3%A9zout%27s_identity