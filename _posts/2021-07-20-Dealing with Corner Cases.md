---
title: "Dealing with Corner Cases"
date: 2021-07-20
categories:
  - blog
tags:
  - algorithm
  - summary
---

1. Check if the index is out of bound when accessing array element
    1. `arr[0]`: check if the array is empty before using this element
    2. `arr[i]`: check if `0 <= i < len(arr)`
    3. Related Problems
        * [LC8. String to Integer (atoi)][LC8. String to Integer (atoi)]

2. Check each branch in your conditional statements, make sure they are correct, and if the final result is obtained by combining several steps together, make sure the final one is correct.

3. When create a list of list, be careful about the sub-list you add to the outer list. You need make a copy of the sub-list when adding it into the outer list. Otherwise, if the sub-list is changed in other parts of the program, the sub-list in the result will change as well.
```
res = []
sublist = [1,2,3]
res.append(sublist.copy()) #remember to use copy here, otherwise you'll get [1,2,3,4] in res
res.append(list(sublist)) #This works as well
res.append(sublist) #This won't work
sublist.append(4)   
```

4. When deal with matrix, consider matrix with only 1 element, 1 row and 1 column. 

5. When check if a binary search tree (BST) is valid or not, make sure that **all nodes**(not just the left child of the root) on the left should be smaller than the root, and **all nodes** on the right should be larger than the root. 
[LC8. String to Integer (atoi)]: https://leetcode.com/problems/string-to-integer-atoi/

6. If you need to update a variable inside a function and the variable is used outside the function as well. Be sure to declare it as `nonlocal` to avoid error. This doesn't apply to mutable types, e.g. `list`.

7. If you are given a class, make sure your instance use the proper arguments, especially don't miss any non-default arguments.



