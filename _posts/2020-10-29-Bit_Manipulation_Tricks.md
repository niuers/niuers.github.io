---
title: "Bit Manipulation Trikcs"
date: 2020-10-29
categories:
  - blog
tags:
  - bit
  - programming
---

1. How to set the rightmost `1-bit` (and all the lower bits as well) to `0`:
    1. `x & (x-1)`
    2. For any number `n`, doing a bit-wise `AND` of `n` and `n-1` flips the least significant (rightmost) `1-bit` in `n` to `0`.
        * The least significant `1-bit` in `n` always corresponds to the rightmost `0-bit` in `n-1`. So `n & n - 1` always flips the least significant `1-bit` in `n` to `0`, sets all the lower bits to `0` and leaves all other higher bits the same.
        * For example, `12 (1100)` & `11 (1011)` = `8(1000)`. The least significant 1-bit (at `2^2` position) in `12` has flipped to `0`.

2. Use `&` to check if a bit is `1` or `0`.
    ```
    #Check the 2^0 position
    mask = 1 #0001
    n = 5  #0101
    n & mask = 1 # n has 1 at 2^0

    #Check the 2^2 position
    mask = 4  #0100
    n = 11 #1011
    n & mask = 0  # n has 0 at 2^2
    ``` 

3. `n/2 = n >> 1` and `n%2 = n & 1`, `2n = n << 1`

4. XOR (Exclusive OR)
    * `a^0 = a`
    * `a^a = 0`
    * `a^b^b = a`

5. `~x & x = 0`

6. Swap without temporary variable
   ```
   a = a^b
   b = a^b  # a^b^b = a
   a = a^b  # a^b^a = b
   ```

7. How to isolate the rightmost 1-bit and set all the other bits to `0`
    1. `-x = ~x + 1`: get the negative of `x` by negating `x` and add `1`. 
        * This is due to "two's complement". 
        * Adding `1` sets the rightmost `0-bit` in `~x` to `1` and set all the lower bits to zero.
        * The rightmost `0-bit` in `~x` is the rightmost `1-bit` in `x`
    2. `x & (-x)`: keep only the rightmost 1-bit 
        * `x` and `-x` only have one bit in common: the rightmost `1-bit`


    h<sub>&theta;</sub>(x) = &theta;<sub>o</sub> x + &theta;<sub>1</sub>x

8. Sum of two binary numbers without using addition
  * `XOR` gives the sum without carry: `a^b`
  * `AND` and shift left by 1 gives the carry: `(a&b)<<1`

Resources:
* [Two Complement Integers by Ben Eater][Two-Complement-Integers]


[Two-Complement-Integers]: https://youtu.be/4qH4unVtJkE