---
title: "Customize Python Sort"
date: 2021-03-22
categories:
  - blog
tags:
  - python
  - sort

1. Sort a list in Python
    ```
    a = [7,5,2,1,10]
    a.sort()
    sorted(a)
    ```
2. Sort by provide `key`
    ```
    a = [(7,3), (2,4), (5,8)]
    a.sort(key=lambda x: x[1])
    a.sort(key=lambda x: (x[1], x[0]))
    ```    

3. Provide a cumstom comparison function
    * Write a comparison function that returns either negative, 0, or positive number, with `(item1, item2)` as arguments
    * Use `functools.cmp_to_key` to change it to key

    ```
    from functools import cmp_to_key

    def comp_build(build1, build2):
        bx1, bh1, is_left1 = build1
        bx2, bh2, is_left2 = build2
        if bx1 != bx2:
            return bx1 - bx2
        
        if is_left1 and is_left2:
            return bh2 - bh1
        if not is_left1 and is_left2:
            return 1
        if is_left1 and not is_left2:
            return -1

        return bh1 - bh2

    a.sort(key=cmp_to_key(comp_build))
    ```







[Python heapq Heap Queue Algorithm]: https://docs.python.org/3/library/heapq.html