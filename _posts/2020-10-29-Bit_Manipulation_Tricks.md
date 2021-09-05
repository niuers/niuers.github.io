---
title: "Bit Manipulation Trikcs"
date: 2020-10-29
categories:
  - blog
tags:
  - bit
  - programming
---


1. Dealing with the right most bit
    1. Set the rightmost `1-bit` (and all the lower bits as well) to `0` (Brian Kernighan's algorithm to Remove the last bit):
        * `n & (n-1)`
            * For any number `n`, doing a bit-wise `AND` of `n` and `n-1` flips the least significant (rightmost) `1-bit` in `n` to `0`.
            * The least significant `1-bit` in `n` always corresponds to the rightmost `0-bit` in `n-1`. So `n & n - 1` always flips the least significant `1-bit` in `n` to `0`, sets all the lower bits to `0` and leaves all other higher bits the same.
            * For example, `12 (1100)` & `11 (1011)` = `8(1000)`. The least significant 1-bit (at `2^2` position) in `12` has flipped to `0`.
    2. Extract the last bit: Isolate the rightmost 1-bit and set all the other bits to `0`
        1. First note that `-x = ~x + 1`:
            * This is due to "two's complement". 
            * Adding `1` sets the rightmost `0-bit` in `~x` to `1` and set all the lower bits to zero.
            * The rightmost `0-bit` in `~x` is the rightmost `1-bit` in `x`
            * This operation reverts all bits of `x` except the rightmost 1-bit.
        2. `x & (-x)` or `A&~(A-1)` or `x^(x&(x-1))`: keep only the rightmost 1-bit 
            * `x` and `-x` only have one bit in common: the rightmost `1-bit`
            * Hence a number is a power of two if `x & (-x) == x` or `x & (x - 1) == 0`
        4. Check if `x` is a power of `4`
            *. If `x & (-x) == x and x ^ (101010...10)==0`, then `x` is power of `4`. Write the number in 16-base, we have `0xaaaaaaaa`
            * If `x` is a power of two and `x % 3 == 1`, then `x` is a power of four.
                * Since if `x = 2^a`. Then `x` is a power of four only if `a` is even
                * Next step is to consider both cases `a = 2k` and `a = 2k + 1`, and to compute `x` modulo after division by three
            * You can also check if `log(n, 4)` is an integer, i.e. `log(n,2)/2` is an integer, i.e. `log(n,2)` is even, i.e. `log(n,2) % 2 ==0 `
    3. Set the `k-th` bit to `1`
        * `bitmask = 1 << k`
    4. Combine bits at different locations into one number
        * `bitmask |= 1 << k`

2. Use `&` to check and set a bit in a number
    ```
    #Check the 2^0 position
    mask = 1 #0001
    n = 5    #0101
    n & mask = 1  #n has 1 at 2^0

    #Check the 2^2 position
    mask = 4  #0100
    n = 11    #1011
    n & mask = 0  # n has 0 at 2^2

    # In general to check if num's k-th bit is 1:
    num & (1<<k)

    # Set the k-th bit of num to 1
    num = num | (1<<k)

    # Unset the k-th bit to 0
    num &= ~(1 << k)
    ```

3. `n//2 = n >> 1` and `n%2 = n & 1`, `2*n = n << 1`

4. XOR (Exclusive OR) operator `^`: 
    * The exclusive-or operation takes two inputs (`x,y`) and returns a 1 if either one or the other of the inputs is a 1, but not if both are. That is, if both inputs are 1 or both inputs are 0, it returns 0. So it keeps the differences between `x` and `y`.
        * If we have `x^y=a`, we can separate the right most bit `1` in `a`, and either `x` or `y` will have that bit, not both of them.
        * `a^0 = a` #appear once
        * `a^a = 0` #appear twice
        * `a^a^a = a` #appear three times
        * `a^b^b = a` 

    * XOR could be used to detect the bit which appears odd number of times: 1, 3, 5, etc. or or save the distinct bits and remove the same.
      * To check the numbers that appear once but not twice, you can use `seen_once = seen_once ^x`, if a number appears twice, `seen_once` will be zero.
      * To check the numbers that appear once but not three times. We can use two variables: 'seen_once', 'seen_twice' etc. The idea is to
          * change `seen_once` only if `seen_twice` is unchanged
          * change `seen_twice` only if `seen_once` is unchanged
          ```
          # To go to the idea of two bitmasks instead of one is not a big deal, basically it's
          # NOT seen_twice AND (CHANGE see_once)
          # NOT seen_once AND (CHANGE see_twice)
          seen_once = seen_twice = 0
          seen_once = ~seen_twice & (seen_once ^ num)
          seen_twice = ~seen_once & (seen_twice ^ num)
          ```
          * This way bitmask seen_once will keep only the number which appears once and not the numbers which appear three times.
      * [Explanation][Explanation for Approach 3: Bitwise Operators : NOT, AND and XOR]: There are 3 key parts:
          * Split each original number into a group of numbers, which are the power of 2. E.g., 5 = 1+4; 7=1+2+4; 8=8
          * Each number after splitting is the power of 2, such as 1,2,4,8,16 .... Use two hash maps to save them.
              * If this is the first time we see a number, save it in hash-map-once.
              * If a number has already been saved in hash-map-once, it means this is the second time we see it. Remove it from hash-map-once and save it in hash-map-twice.
              * If a number has already been in hash-map-twice, it means this is the third time we see it. Remove it from hash-map-twice and we are done with it. This number has been removed from both hash maps.
          * After processing all numbers, hash-map-once only contains the group of power-of-two numbers splitted from the single orgininal number. hash-map-twice is 0. We could simply collect all numbers in hash-map-once and add them together to get the single original number.
          * [Optimization] Because all numbers after splitting are the power of 2, such as 1,2,4,8,16, etc., we assume there are at most 32 types of numbers after splitting. We could save memory by squashing the two hash maps into two 32-bit integers. Each power-of-2 number could be represented by 1 bit in the 32-bit integer.
              * hash-map-once -> seenOnce
              * hash-map-twice -> seenTwice
              * After processing all numbers, the value of integer seenOnce is exactly the sum of all numbers left in hash-map-once.
          * Further thoughts:
              * It is not necessary to replace the two hash-maps with two 32-bit integers. If we simply use 1 hash-map to save the occurrences of all power-of-2 numbers, the size of the hash-map is at max 32. We can still consider it as a constant memory space solution and the space complexity is still O(0). With the hash map, we could easily extend the problem to n duplicated numbers. E.g., All numbers are duplicated 100 times except 1. Find out this single number.
        * [Another explanation][LeetCode #137 Single Number II]


5. `~x & x = 0`

6. Swap without temporary variable
   ```
   a = a^b
   b = a^b  # a^b^b = a
   a = a^b  # a^b^a = b
   ```

h<sub>&theta;</sub>(x) = &theta;<sub>o</sub> x + &theta;<sub>1</sub>x

7. Sum of two binary numbers without using addition
  * `XOR` gives the sum without carry: `a^b`
  * `AND` and shift left by 1 gives the carry: `(a&b)<<1`
  * Problems
      * [LC67. Add Binary][LC67. Add Binary]

8. Right shifting operations on negative values are undefined
    * One potential pitfall with the right-shift operator is using it on negative odd numbers. Two's complement makes the result one-off what you would expect/ probably wanted. The solution is to add 1 before doing the bit-shift on a negative number. This way, it'll be "correct" regardless of whether the number was odd or even. See [LC29. Divide Two Integers][LC29. Divide Two Integers]
    ```
    int a = -1020;
    a = a >> 1;
    System.out.println(a);
    // Prints -510. Great!
    int b = -1021;
    b = b >> 1;
    System.out.println(b);
    // Prints -511. Ugghh.
    ```

    ```
    int a = -1020;
    a = (a + 1) >> 1;
    System.out.println(a);
    // Prints -510. Great!
    int b = -1021;
    b = (b + 1) >> 1;
    System.out.println(b);
    // Prints -510. Yay!
    ```

9. Get all 1-bit: `~0`

10. Keep as many 1-bits as possible using `|`

11. Sets ([A summary: how to use bit manipulation to solve problems easily and efficiently][A summary: how to use bit manipulation to solve problems easily and efficiently])
    1. All the subsets: A big advantage of bit manipulation is that it is trivial to iterate over all the subsets of an N-element set: every N-bit value represents some subset. Even better, if A is a subset of B then the number representing A is less than that representing B, which is convenient for some dynamic programming solutions.
    2. It is also possible to iterate over all the subsets of a particular subset (represented by a bit pattern), provided that you don’t mind visiting them in reverse order (if this is problematic, put them in a list as they’re generated, then walk the list backwards). The trick is similar to that for finding the lowest bit in a number. If we subtract 1 from a subset, then the lowest set element is cleared, and every lower element is set. However, we only want to set those lower elements that are in the superset. So the iteration step is just `i = (i - 1) & superset`.

12. Python related
    1. Convert an integer to binary string: `bin(a)`
        * The binary string prefixed with “0b”.
        ```
        bin(3)   #'0b11'
        bin(-10) #'-0b1010'
        ```
        * If the integer is negative, you need subtract it from power of 2
        ```
        print(bin(-7))           # -0b111: not what we want
        print(bin((1 << 8) - 7)) # 0b11111001, two's complement representation with 8-bit
        print(bin((1 << 16) - 7)) # 0b1111111111111001, two's complement representation with 16-bit
        ```
        * To convert from binary representation to integer
        ```
        print(0b111)           # 7
        print(-0b111)          # -7
        print(0b11111001-pow(2,8))  #-7
        ```
    2. Convert a binary string to integer: `int(s, 2)`, e.g. `int('111', 2)` returns `7`.

13. Pay attention to the operator precendence
    1. The precendence of bit operators `&`, `|` etc. are lower than `+`, `-` etc. So make sure to use parentheses around bit operators. For example:
        * `res = res*2 + n & 1`: it will compute `res*2+n` first, then `&` with `1`. To correct it, we should use `res = res*2 + (n & 1)` instead.

14. Retrieve the right most byte of a number
    1. `n & 0xff` or `n & 11111111`

15. Swap the first 16-bit with the last 16-bit in a number
    1. `n = (n >> 16) | (n << 16)`
    2. `n = ((n & 0xff00ff00) >> 8) | ((n & 0x00ff00ff) << 8)`: swap the first 8 bits with the 2nd 8 bits, and 3rd 8 bits with the 4th 8 bits.   
        * `0x` means hexidecimal number (base 16) 

16.  Convert between big-endian and little-endian
    1. In different architectures, the multi-byte data can be stored in two different ways. Sometimes the higher order bytes are stored first, in that case these are known as big endian, and sometimes the lower order bytes are stored first, then it is called little endian.
    2. N.B. The endians happen in byte-level
    3. To do this we have to interchange the 1st and 4th bytes, and 2nd and 3rd bytes.
    ```
    swapped = ((num>>24)&0xff) | // move byte 3 to byte 0
              ((num<<8)&0xff0000) | // move byte 1 to byte 2
              ((num>>8)&0xff00) | // move byte 2 to byte 1
              ((num<<24)&0xff000000); // byte 0 to byte 3
    ```


Resources:
* [Two Complement Integers by Ben Eater][Two-Complement-Integers]
* [Bit Twiddling Hacks][Bit Twiddling Hacks]
* [Explanation for Approach 3: Bitwise Operators : NOT, AND and XOR][Explanation for Approach 3: Bitwise Operators : NOT, AND and XOR]
* [A summary: how to use bit manipulation to solve problems easily and efficiently][A summary: how to use bit manipulation to solve problems easily and efficiently]
* [How do I convert between big-endian and little-endian values in C++?][How do I convert between big-endian and little-endian values in C++?]


[Two-Complement-Integers]: https://youtu.be/4qH4unVtJkE
[LC29. Divide Two Integers]: https://leetcode.com/problems/divide-two-integers/
[A summary: how to use bit manipulation to solve problems easily and efficiently]: https://leetcode.com/problems/sum-of-two-integers/discuss/84278/A-summary%3A-how-to-use-bit-manipulation-to-solve-problems-easily-and-efficiently
[LC67. Add Binary]: https://leetcode.com/problems/add-binary/
[Explanation for Approach 3: Bitwise Operators : NOT, AND and XOR]: https://leetcode.com/problems/single-number-ii/solution/563404
[LeetCode #137 Single Number II]: https://lenchen.medium.com/leetcode-137-single-number-ii-31af98b0f462
[Bit Twiddling Hacks]: http://graphics.stanford.edu/~seander/bithacks.html#ReverseByteWith64BitsDiv
[How do I convert between big-endian and little-endian values in C++?]: https://www.tutorialspoint.com/how-do-i-convert-between-big-endian-and-little-endian-values-in-cplusplus