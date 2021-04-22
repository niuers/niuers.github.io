---
title: "Small Functions in Python"
date: 2021-04-21
categories:
  - blog
tags:
  - algorithm
  - leetcode
  - python
  - summary
---

1. Generate a list of consecutive integers 
    ```
    a = list(range(1,10,2))
    ```
2. Convert an array of integers to string and join them into a large string:
    ```
    a = list(range(1,10,2))
    s = ''.join(map(str, a))
    ```
3. Binary/Hexidecimal numbers
    1. Convert integer to binary/hexidecimal string
        * `bin(255)` # print out `0b11111111`
        * `hex(255)` # print out `0xff`
    2. Convert binary/hexidecimal string to integer
        * `int('0b11111111', 2)` # print out `255`
        * `int('0xff', 16)` #print out `255`

4. Encode a 32-bit integer to a 4-byte string
    1. Encode
    ```
    def int_to_str(x):
        """
        Encodes integer to bytes string
        """
        #Convert each byte into a character
        bytes = [chr(x >> (i * 8) & 0xff) for i in range(4)]
        bytes.reverse()
        bytes_str = ''.join(bytes)
        return bytes_str            
    ```
    2. Decode
    ```
    def str_to_int(bytes_str):
        """
        Decodes bytes string to integer.
        """
        result = 0
        for ch in bytes_str:
            result = result * 256 + ord(ch)
        return result
    ```

5. Reverse a list
  ```
  a.reverse()  #returns None, reverse the list in-place
  b = a[::-1]  #returns a new list
  ```
