---
title: "Python Libraries"
date: 2021-05-05
categories:
  - blog
tags:
  - python
  - summary
---

1. OrderedDict:
    1. Python Source Code for OrderedDict: [Python OrderedDict Source]
    2. The OrderedDict is all about recording insertion order. If any other order is of interest, then another structure (like an in-memory dbm) is likely a better fit.
    3. [What are the trade-offs of the possible underlying data structures?][Python OrderedDict Tradeoff]
        * Keeping a sorted list of keys is fast for all operations except `__delitem__()` which becomes an `O(n)` exercise. This data structure leads to very simple code and little wasted space.
        * Keeping a separate dictionary to record insertion sequence numbers makes the code a little bit more complex. All of the basic operations are `O(1)` but the constant factor is increased for `__setitem__()` and `__delitem__()` meaning that every use case will have to pay for this speedup (since all buildup go through `__setitem__`). Also, the first traveral incurs a one-time `O(n log n)` sorting cost. The storage costs are double that for the sorted-list-of-keys approach.
        * A version written in C could use a linked list. The code would be more complex than the other two approaches but it would conserve space and would keep the same big-oh performance as regular dictionaries. It is the fastest and most space efficient.



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
    Frozen set is just an immutable version of a Python set object. While elements of a set can be modified at any time, elements of the frozen set remain the same after creation. Due to this, frozen sets can be used as keys in Dictionary or as elements of another set. But like sets, it is not ordered (the elements can be set at any index).

    3. `set` operations time complexity
        * union `s|t`: `O(len(s)+len(t))`
        * Intersection `s&t`: `O(min(len(s), len(t)))`
        * `x in s`: `O(1)` in average, but `O(n)` in worst case
        * Difference `s-t`: `O(len(s))`

    4. `setdefault(key[, default])`
        If `key` is in the dictionary, return its value. If not, insert key with a value of `default` and return `default`. `default` defaults to `None`.


7. `heappush` and `heappop`
    1. `O(log n)` push and `O(log n)` pop.


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
    2. 


[Python OrderedDict Source]: https://github.com/python/cpython/blob/226a012d1cd61f42ecd3056c554922f359a1a35d/Objects/odictobject.c
[RealPython Defaultdict]: https://realpython.com/python-defaultdict/#diving-deeper-into-defaultdict
[Python OrderedDict Tradeoff]: https://www.python.org/dev/peps/pep-0372/