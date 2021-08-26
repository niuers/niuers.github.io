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

8. When you are trying to make sure that there's a one-to-one match between two sets of arrays using hash map, don't forget to check the reverse match, i.e. don't just check one-direction match. For example, if we have `a->1`, `a->2` can be checked by a hash map from letter to number, but if there's `b->1`, it won't work. We should check that `1` doesn't already has a match to `a`. See [LC290 Word Pattern][LC290. Word Pattern].

9. When you are dealing with a matrix, i.e. a 2D array in Python, be careful when you want to extract the columns from the matrix, because this `matrix[:][1]` doesn't work. You have to extract the elements explicitly, or use `numpy`.
    ```
    matrix = [[1,4,7,11,15],[2,5,8,12,19],[3,6,9,16,22],[10,13,14,17,24],[18,21,23,26,30]]
    print(matrix[1][:])  # print out row 1, [2, 5, 8, 12, 19]
    print(matrix[:][1])  # still print out row 1, [2, 5, 8, 12, 19], not the column 1 as you would expect
    ```

10. When you are dealing with a list of list, consider the cases where the inner lists can be empty.

[LC290. Word Pattern]: https://leetcode.com/problems/word-pattern/

