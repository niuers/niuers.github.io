---
title: "Bit Manipulation Trikcs"
date: 2020-10-29
categories:
  - blog
tags:
  - bit
  - programming
---

1. For any number `n`, doing a bit-wise `AND` of `n` and `n-1` flips the least significant 1-bit in `n` to `0`.
    * The least significant 1-bit in `n` always corresponds to a 0-bit in `n-1`. So `n & n - 1` always flips the least significant 1-bit in `n` to `0`, and leaves all other bits the same.
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

7. Isolate the right most 1-bit
    * `-x = ~x + 1`: get negative `x`
    * `x & (-x)`: keeps only the right most 1-bit


Resources:
* [Two Complement Integers by Ben Eater][Two-Complement-Integers]


[Two-Complement-Integers]: https://youtu.be/4qH4unVtJkE