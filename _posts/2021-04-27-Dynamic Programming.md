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


2. How to realize that a problem is NOT a dynamic programming problem? 
    1. [One way to realize that it isn't dynamic programming][LC1631. Path With Minimum Effort] is to notice that the hiker can go in all four directions. This means that a dp algorithm would need to look into subproblems that haven't been solved yet.



3. Different solutions


4. Mistakes

5. Problem Type
    
6. Similar Problems

7. Template

8. I understand the solution, but HOW do I think to GET there myself?
    1. Where could you improve?
    2. What questions should I ask myself so that I push myself closer to the solution? 
    3. What conclusions did I reach that I dropped some idea for the other?
    4. How can I reach this conclusion faster ?
    




[LC1631. Path With Minimum Effort]: https://leetcode.com/problems/path-with-minimum-effort/solution/