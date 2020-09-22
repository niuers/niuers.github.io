---
title: "Python Copy: Shallow and Deep"
date: 2020-09-22
categories:
  - blog
tags:
  - python
---

In python we have so-called 'deep copy' and 'shallow copy', [for example][python-example]:

```
import copy
x = copy.copy(y)       # shallow copy of y
x = copy.deepcopy(y)   # deep copy of y
```

> [The difference between shallow and deep][shadow-deep-diff] copying is only relevant for compound objects (objects that contain other objects, like `list`, `dict`, `set`, `tuple` and `bytearray` or class instances).
- A shallow copy constructs a new compound object and then (to the
  extent possible) inserts *the same objects* into it that the
  original contains.
- A deep copy constructs a new compound object and then, recursively,
  inserts *copies* into it of the objects found in the original.

Notes:
1. For `list`, `dict`, `set` and `bytearray`, `copy.copy` is equivalent to `list.copy`, `dict.copy`, `set.copy` and `bytearray.copy` respectively. 
That is, all the class method `copy` of `list`, `dict`, `set` and `bytearray` are shallow copy.
1. Shallow copy is an `O(N)` complexity algorithm where `N` is the length of the original compound object. Shallow copy needs to allocate at least size of `N` of `PyBoject*` type in memory and loop to assign.
1. Deep copy is an `O(NM)` complexity algorithm where `N` is the length of the original compound object, and `M` is the average length (in terms of non-compound objects) of the elements in the compound. 
1. The shallow and deep copy for non-compound objects are the same, for example, `int`, `float`, `str` etc.
1. `list.copy` is the same as using slice, i.e. `a[:]`


[python-example]: https://github.com/python/cpython/blob/d986d1657e1e7b50807d0633cb31d96a2d866d42/Lib/copy.py#L8

[shadow-deep-diff]: https://github.com/python/cpython/blob/d986d1657e1e7b50807d0633cb31d96a2d866d42/Lib/copy.py#L12