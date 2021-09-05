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

    #Note, join requires all elements to be string type, you can't join with numerical or None
    a = ['abc', None, 'efg']
    print(''.join(a)) # TypeError: sequence item 1: expected str instance, NoneType found
    ```
    * If you join on an array with a single element, you get the single string back (i.e. no join happens)
    ```
    a = ['']
    '/'.join(a) # returns ''

    a = ['root']
    s = '/'.join(a) # returns 'root'

    a = ['', 'root']
    s = '/'.join(a) # returns '/root'
    ```

3. Binary/Hexidecimal numbers
    1. Convert integer to binary/hexidecimal string
        * `bin(255)` # print out `0b11111111`
        * `hex(255)` # print out `0xff`
    2. Convert binary/hexidecimal string to integer
        * `int('0b11111111', 2)` # print out `255`
        * `int('0xff', 16)` #print out `255`

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

7. Python `split(sep=None, maxsplit=-1)` needs a separator to work properly
    * If `sep` is given, consecutive delimiters are not grouped together and are deemed to delimit empty strings (for example, `'1,,2'.split(',')` returns `['1', '', '2']`). The `sep` argument may consist of multiple characters (for example, `'1<>2<>3'.split('<>')` returns `['1', '2', '3']`). Splitting an empty string with a specified separator returns `['']`.

    ```
    a = '12345'
    m = [int(k) for k in a.split()]
    print(m) # print out [12345] since there's no whitespace, which is default if sep is not given
    # Not the [1,2,3,4,5] as you might have thought

    print(a.split(',')) #print out ['12345'] #No comma neither

    #Note there's an empty string at index 0 and the end
    a = '/leet/code/'
    print(a.split('/')) # ['', 'leet', 'code', '']

    #Note the size is 2 here
    a = '/'
    print(a.split('/)) # ['', '']

    #Also compare following two cases
    a = '  a  '.split(' ') #each whitespace is treated separately
    print(len(a), a) # 5 ['', '', 'a', '', '']
    a = '  a  '.split() #whitespaces are consolidated and treated as one
    print(len(a), a) #1 ['a']

    #You can't specify an empty separator ''
    a.split('') #ValueError: empty separator

    ```

    * If `sep` is not specified or is `None`, a different splitting algorithm is applied: runs of consecutive whitespace are regarded as a single separator, and the result will contain no empty strings at the start or end if the string has leading or trailing whitespace. Consequently, splitting an empty string or a string consisting of just whitespace with a `None` separator returns `[]`.
    ```
    print('  abc  def  '.split()) # ['abc', 'def']
    print('   '.split())  # []
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

16. `break` a loop:

```
for i in range(5):
    print(f"i = {i}")
    j = i
    #while j < 5:        
    for j in range(i, 5):
        if j >= 3:
            break    #This will break the inner-for/inner-while loop only
        else:
            j += 1
        print(f"--- j = {j}")
```

17. Create a counter
```
import itertools as it
# odds = it.count(start=1, step=2)

index = {}
count = itertools.count()
for p in pair:
    if p not in index:
        index[p] = next(count)            
```            

18. Upack a list of list
```
workers = [[1,2],[2,3],[5,3],[3,7], [0,3]]
for wi, (wx, wy) in enumerate(workers): #Have to use () or [] here to upack
    print(wi, wx, wy)
```

19. Convert a number to string and a string to number
```
input = 12345
iter = map(int, str(input))
#'map' object is not subscriptable
# print(iter[0], iter[3]) #This throws Error

#Better to use this:
arr = list(str(input))
output = int("".join(arr))

```

20. Check if a string is numerical, alphabet
    1. `str.isalnum()`: Return `True` if **all characters** in the string are alphanumeric and there is at least one character, `False` otherwise. A character `c` is alphanumeric if one of the following returns `True`: `c.isalpha()`, `c.isdecimal()`, `c.isdigit()`, or `c.isnumeric()`.

21. Convert a string to lower/upper case
    ```
    str.lower()
    str.upper()
    ```

22. `strip([chars])` will remove both leading and trailing characters    

23. `log(x, base)`
    * With one argument, return the natural logarithm of `x` (to base `e`).
    * With two arguments, return the logarithm of `x` to the given base, calculated as `log(x)/log(base)`.

24. Python swap doesn't work with embeded index
    ```
    nums[0], nums[nums[0]] = nums[nums[0]], nums[0] #won't work, nums[0] will be changed, but nums[nums[0]] wont
    nums[nums[0]], nums[0] = nums[0], nums[nums[0]] #This works
    ```

25. Remove an element from list
    1. `my_list.pop(index)`    