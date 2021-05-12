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

6. Don't use mutable type as default parameter value in Python
  ```  
  class A:
      def __init__(self, links={}):
          self.links = links

  a = A()
  a.links['member'] = 'yes'
  b = A()
  print(a.links, b.links)
  >>> {'member': 'yes'} {'member': 'yes'}
  ```

  You can see that instances `a` and `b` have the same member `links`, which is wrong.
  The mutable types are: list, dictionary, set and user-defined classes etc.
  This is not a problem for immutable types, e.g. integer, float, tuple, string, range etc. 

7. Python `split()` needs a separator to work properly
```
a = '12345'
m = [int(k) for k in a.split()]
print(m) # print out [12345]
# Not the [1,2,3,4,5] as you have thought before
```

8. Unpack Python tuple/list
```
m = (5,3)
x, y = m

m = [5,3,2]
x,y,z = m
```

9. Compute the quotient and remainder for an integer
    * For integers, the result is the same as `(a // b, a % b)`.
```
#quotient, remainder = divmod(dividend, divisor)
divmod(11,3)  # (3,2)
divmod(-11,3) # (-4,1)
```

10. `//` floor division
    * It rounds down to the nearest integer. (although a float is returned when used with floats)
```
print(3//2)       # 1
print(-3//2)      # -2
print(2.0//-3)    #-1.0
print(-3.0//2)    #-2.0
```

11. Local and non-local variables in Python functions
```
def outer():
    const_var = 5
    nonconst_var = 8
    print(f"Original values: const_var = {const_var}, nonconst_var={nonconst_var}")
    arr = [1]
    def helper():
        # Following `nonlocal` declaration is needed to avoid Error, 
        # UnboundLocalError: local variable 'nonconst_var' referenced before assignment  `nonconst_var += const_var`
        # This is because `nonconst_var` is modified in the inner() function
        # This is not needed for `const_var` which is not modified

        nonlocal nonconst_var
        nonconst_var += const_var
        arr.append(const_var)
        arr.append(nonconst_var)
        print(f"const_var = {const_var}, nonconst_var={nonconst_var}")

        # However, notice, nonlocal is not needed for container types, i.e. list, set, dict etc.
        print(arr)
        return const_var, nonconst_var
    
    helper()
    
outer()     

# Output
>> Original values: const_var = 5, nonconst_var=8
>> const_var = 5, nonconst_var=13
>> [1, 5, 13]
```

12. Python Set Operations
```
C = A | B # Union
C = A.union(y)
C = A & B # Intersection
C = A.intersection(B)	
C = A - B # Difference
C = A.difference(B)
C = A ^ B # Symmetric difference
C = A.symmetric_difference(B)	
```

13. Python array slicing can go out of bounds: If the bounds in slice are out of the range, it returns empty list or string.
```
word = [1,2,3,4,5] #'abcde'
print(word[:0]) # []
print(word[4:]) # 5
print(word[9:]) # []
```

14. Check if the string is digit:
```
str.isdigit()
#Return True if all characters in the string are digits and there is at least one character, False otherwise.


```

15. Return the indexes of sorted list
```
s = [2, 3, 1, 4, 5, 3]
sorted(range(len(s)), key=lambda k: s[k])
>>> [2, 0, 1, 5, 3, 4]

```