---
title: "Python Libraries"
date: 2021-05-05
categories:
  - blog
tags:
  - python
  - summary
---

1. `OrderedDict`:
    1. [Python Source Code for OrderedDict][Python OrderedDict Source]:
    2. The OrderedDict is all about recording insertion order. If any other order is of interest, then another structure (like an in-memory dbm) is likely a better fit.
    3. [What are the trade-offs of the possible underlying data structures?][Python OrderedDict Tradeoff]
        * Keeping a sorted list of keys is fast for all operations except `__delitem__()` which becomes an `O(n)` exercise. This data structure leads to very simple code and little wasted space.
        * Keeping a separate dictionary to record insertion sequence numbers makes the code a little bit more complex. All of the basic operations are `O(1)` but the constant factor is increased for `__setitem__()` and `__delitem__()` meaning that every use case will have to pay for this speedup (since all buildup go through `__setitem__`). Also, the first traveral incurs a one-time `O(n log n)` sorting cost. The storage costs are double that for the sorted-list-of-keys approach.
        * A version written in C could use a linked list. The code would be more complex than the other two approaches but it would conserve space and would keep the same big-oh performance as regular dictionaries. It is the fastest and most space efficient.
    4. This can be used to implement LRU cache.
    5. Member methods
        * `popitem(last=True)`: The `popitem()` method for ordered dictionaries returns and removes a `(key, value)` pair. The pairs are returned in LIFO order if last is true or FIFO order if false.
        ```
        key, v = my_ordered_dict.popitem(last=False)
        ```
        * `move_to_end(key, last=true)`: Move an existing key to either end of an ordered dictionary. The item is moved to the right end if last is true (the default) or to the beginning if last is false. Raises `KeyError` if the key does not exist:
    6. If one would need a structure, which provides four operations in `O(1)` time :
        * Insert the key
        * Get the key and check if the key exists
        * Delete the key
        * Return the first or last added key/ value
        * The first three operations in `O(1)` time are provided by the standard hashmap, and the forth one - by linked list.
        * There is a structure called ordered dictionary, it combines behind both hashmap and linked list. In Python this structure is called `OrderedDict` and in Java LinkedHashMap.
    7. Problems
        1. [340. Longest Substring with At Most K Distinct Characters][340. Longest Substring with At Most K Distinct Characters]
2. `dictionary`: Python 3.7 makes it a language feature that dictionaries are 'insertion ordered'
   * `my_dict.pop(key, default_value)`: `O(1)` in average, `O(n)` in worst
   * `my_dict.popitem()`: remove the last inserted item

2. deque
    1. Initialize
    `dq = deque([(0,0)])` # Initialize the deque with 1 tuple element
    2. dequeuing: `popleft()`
    3. enqueuing: `append()`, append to the right

3. defaultdict
    1. [`default_factory`][RealPython Defaultdict]: Holds the callable invoked by `.__missing__()` to automatically provide default values for missing keys. 
        * The first argument to the Python defaultdict type must be a callable that takes no arguments and returns a value. This argument is assigned to the instance attribute, `.default_factory`. The default value of `.default_factory` is `None`.
        * If you instantiate `defaultdict` without passing a value to `.default_factory`, then the dictionary will behave like a regular `dict` and the usual `KeyError` will be raised for missing key lookup or modification attempts
        ```
        >>> from collections import defaultdict
        >>> dd = defaultdict()
        >>> dd['missing_key']
        Traceback (most recent call last):
          File "<stdin>", line 1, in <module>
            dd['missing_key']
        KeyError: 'missing_key'
        ```
        * Note: If you initialize a defaultdict using a valid callable, then you won’t get a KeyError when you try to get access to a missing key. Any key that doesn’t exist gets the value returned by `.default_factory`. 
        * Keep in mind that `.default_factory` is only called from `.__getitem__()` and not from other methods. This means that if `dd` is a `defaultdict` and `key` is a missing key, then `dd[key]` will call `.default_factory` to provide a default value, but `dd.get(key)` still returns `None` instead of the value that `.default_factory` would provide. That’s because `.get()` doesn’t call `.__getitem__()` to retrieve the key.  

    2. Automatically increase the values in the `defaultdict`: Every time a new item is inserted into the dictionary, its value is the current size of the dictionary, which automatically increases 1 with each new item.
    ```
    trees = defaultdict()
    trees.default_factory = trees.__len__
    print(trees[7], len(trees)) #0 1
    print(trees[5], len(trees)) #1 2
    ```
    3. Remove an item from `defaultdict` or `dict`
        1. Use `del d[key]`: Remove `d[key]` from `d`. Raises a `KeyError` if key is not in the map.
        2. Use `d.pop(key[, default])`: If `key` is in the dictionary, remove it and return its value, else return `default`. If `default` is not given and key is not in the dictionary, a `KeyError` is raised.
    4. It's okay to use `None` or empty string `''` as key
    5. You can declare a `graph = defaultdict(defaultdict)` then, `graph[v1][v2] = 1.0`


4. `bisect_left(a, x, lo=0, hi=len(a))` and `bisect_right(a, x, lo=0, hi=len(a))`
    1. Note they only work with **ascending** ordered list, not **descending** ordered list

5. `itertools`
    1. `itertools.groupby(iterable, key=None)`
    ```
    # [k for k, g in groupby('AAAABBBCCDAABBB')] --> A B C D A B
    # [list(g) for k, g in groupby('AAAABBBCCD')] --> AAAA BBB CC D
    groups = []
    uniquekeys = []
    data = sorted(data, key=keyfunc)
    for k, g in groupby(data, keyfunc):
        groups.append(list(g))      # Store group iterator as a list
        uniquekeys.append(k)    
    ```

    2. combinatoric iterators
        * `product(*iterables, repeat=1)`: Cartesian product of input iterables. Roughly equivalent to nested for-loops in a generator expression. For example, product(A, B) returns the same as ((x,y) for x in A for y in B).

        To compute the product of an iterable with itself, specify the number of repetitions with the optional repeat keyword argument. For example, product(A, repeat=4) means the same as product(A, A, A, A)

        ```
        # product('ABCD', 'xy') --> Ax Ay Bx By Cx Cy Dx Dy
        # product(range(2), repeat=3) --> 000 001 010 011 100 101 110 111
        ```


        * `permutations(iterable, r=None)`: Return successive `r` length permutations of elements in the iterable.
        ```
        # permutations('ABCD', 2) --> AB AC AD BA BC BD CA CB CD DA DB DC
        # permutations(range(3)) --> 012 021 102 120 201 210
        ```
        * `combinations(iterable, r)`: Return r length subsequences of elements from the input iterable. The combination tuples are emitted in lexicographic ordering according to the order of the input iterable. So, if the input iterable is sorted, the combination tuples will be produced in sorted order.
        ```
        # combinations('ABCD', 2) --> AB AC AD BC BD CD
        # combinations(range(4), 3) --> 012 013 023 123

        ```
        * `combinations_with_replacement(iterable, r)`: Return r length subsequences of elements from the input iterable allowing individual elements to be repeated more than once.

        ```
         # combinations_with_replacement('ABC', 2) --> AA AB AC BB BC CC
        ```
    

6. `set`/`dict`: 
    1. Can't add/remove items into/from a `set`/`dict` while iterating on it

    ```
    a = set([1,2,3])
    for i in a:
        a.add(i+9) # RuntimeError: Set changed size during iteration
        a.remove(i) # RuntimeError: Set changed size during iteration

    # Similarly we have RuntimeError for dict
    a = {1:'a', 2:'b'}
    for i, v in a.items():
        a['3']='c'
        del a[1]    
    ```

    2. `frozenset`: 
        * Frozen set is just an immutable version of a Python set object. While elements of a set can be modified at any time, elements of the frozen set remain the same after creation. Due to this, frozen sets can be used as keys in Dictionary or as elements of another set. But like sets, it is not ordered (the elements can be set at any index).

    3. `set` operations time complexity
        * union `s|t`: `O(len(s)+len(t))`
        * Intersection `s&t`: `O(min(len(s), len(t)))`, worst case `O(len(s)*len(t))`
        * `x in s`: `O(1)` in average, but `O(n)` in worst case
        * Difference `s-t`: `O(len(s))`

    4. dictionary `setdefault(key[, default])`
        If `key` is in the dictionary, return its value. If not, insert key with a value of `default` and return `default`. `default` defaults to `None`.
    5. Get an element from a `set`
    ```
    item = next(iter(s))
    ```
    6. `set`/`dict` lookup is `O(1)` amortized time, but it can be `O(n)` in worst-case if collision happens.
    7. You can't add a set into another set: 
        * Raise TypeError: unhashable type 'set'
    8. You can't add  list into a set, need to change them to tuple
        * `my_set.add(tuple(my_list))`
    9. [DO NOT MODIFY (add/remove element) a set or dictionary or list while loop within it][Updating a set while iterating over its elements]. The behavior is "undefined"
    ```
    for num in num_set: # use list(num_set) instead
        track.append(num)
        num_set.remove(num)                
        backtrack(num_set, track)                
        num_set.add(num)
        track.pop()
    ```

7. `heappush` and `heappop`
    1. `O(log n)` push and `O(log n)` pop.
    2. Use class to specify the comparison among items, e.g. create a max-heap on `str` type instead of the default min-heap

    ```
    pq = []
    heapq.heappush(pq, MyMaxClass(input))

    class MyMaxClass(str):
        def __init__(self, s): self.s = s
        def __lt__(self,other): return self.s > other.s
        def __eq__(self,other): return self.s == other.s
    ```


8. Python `TreeMap`

9. Greatest common divisor (GCD)
```
import math
math.gcd(12,8) # returns 4
```

10. Python list
    1. The `index()` method returns the position at the first occurrence of the specified value.
    ```
    a = [0,3,2,1,5]
    a.index(1)  #returns 3
    ```
    2. Remove elements in the middle of a list
    ```
    a = [0,3,2,1,5]
    a[1:3] = []
    print(a) # [0, 1, 5], elements a[1], a[2] are removed
    ```
    3. Remove an element at certain index
    ```
    array.pop(remove_idx)  # `O(n)` complexity
    ```


12. `lru_cache(maxsize=128, typed=False)`: Least-recently-used cache decorator
    1. If `maxsize` is set to `None`, the LRU features are disabled and the cache can grow without bound.
    2. Python implements it using double linked list.

13. [Python `dict` keeps insertion order since 3.7][Are dictionaries ordered in Python 3.6+?]
    1. They are insertion ordered. With the existence of OrderedDict, "ordered" suggests further behavior that the `dict` object *doesn't provide*. OrderedDicts are reversible, provide order sensitive methods and, mainly, provide an order-sensive equality tests (`==`, `!=`). `dict`s currently don't offer any of those behaviors/methods.

14. Python `pow(base, exp[, mod])`
    * Return `base` to the power `exp`; if `mod` is present, return `base` to the power `exp`, modulo `mod` (computed more efficiently than pow(base, exp) % mod). The two-argument form `pow(base, exp)` is equivalent to using the power operator: `base**exp`.

15. Check a string is alpha, numeric or not:
    * `s.isalnum()`

16. [Python `str` slice complexity][Time complexity of string slice]
    * Short answer: `str` slices, in general, copy.
    * Long answer: (C)Python `str` do not slice by referencing a view of a subset of the data. There are exactly three modes of operation for `str` slicing:
        * Complete slice, e.g. `mystr[:]`: Returns a reference to the exact same `str` (not just shared data, the same actual object, `mystr` is `mystr[:]` since `str` is immutable so there is no risk to doing so)
        * The zero length slice and (implementation dependent) cached length 1 slices; the empty string is a singleton (`mystr[1:1]` is `mystr[2:2]` is `''`), and low ordinal strings of length one are cached singletons as well (on CPython 3.5.0, it looks like all characters representable in latin-1, that is Unicode ordinals in range(256), are cached)
        * All other slices: The sliced `str` is copied at creation time, and thereafter unrelated to the original `str`. The reason why #3 is the general rule is to avoid issues with large `str` being kept in memory by a view of a small portion of it. If you had a 1GB file, read it in and sliced it like so. then you'd have 1 GB of data being held in memory to support a view that shows the final 1 KB, a serious waste. Since slices are usually smallish, it's almost always faster to copy on slice instead of create views. It also means `str` can be simpler; it needs to know its size, but it need not track an offset into the data as well.
    * N.B. Get a slice from a list is on average the length of the slice, i.e. `O(end-start)`



[Python OrderedDict Source]: https://github.com/python/cpython/blob/226a012d1cd61f42ecd3056c554922f359a1a35d/Objects/odictobject.c
[RealPython Defaultdict]: https://realpython.com/python-defaultdict/#diving-deeper-into-defaultdict
[Python OrderedDict Tradeoff]: https://www.python.org/dev/peps/pep-0372/
[340. Longest Substring with At Most K Distinct Characters]: https://leetcode.com/problems/longest-substring-with-at-most-k-distinct-characters/
[Are dictionaries ordered in Python 3.6+?]: https://stackoverflow.com/questions/39980323/are-dictionaries-ordered-in-python-3-6
[Time complexity of string slice]: https://stackoverflow.com/questions/35180377/time-complexity-of-string-slice
[Updating a set while iterating over its elements]: https://stackoverflow.com/questions/48018680/updating-a-set-while-iterating-over-its-elements