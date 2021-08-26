---
title: "Parse Expressions"
date: 2021-04-27
categories:
  - blog
tags:
  - algorithm
  - summary
---

1. Expression Parsing
    1. Two stacks: operators and parentheses stack and numbers stack
    2. Standard parser: Call parse-functions on those with the lowest precendence and recursively invoke parse-functions of things with higher precendence.
    3. Recursion
    3. [Build Binary Expression Tree From Infix Expression (LC1597)][LC1597]:

2. Evaulate expressions without parentheses
    1. Use a deque: compute the values for each `*` and `/`, push them back, then compute the final results from front to end
    2. Use a stack: convert numbers with `-` to negative numbers and do it similarly as above
    3. No stack: use variables, `last_number`, `current_number`, `sign`, `current_char` to evaulate the expression.
        * N.B. You can compute each number digit by digit

3. Different ways to add parentheses
    1. Split the string with the operators, and recursively call on each substrings
    2. problems
        * [LC241. Different Ways to Add Parentheses][LC241. Different Ways to Add Parentheses]


[LC241. Different Ways to Add Parentheses]: https://leetcode.com/problems/different-ways-to-add-parentheses/


