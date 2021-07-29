---
title: "Balance of Parentheses Problems"
date: 2021-07-17
categories:
  - blog
tags:
  - algorithm
  - summary
---

1. Check if an expression is valid parentheses expression
  1. Keep track of the balance of the string: 
      1. The number of '('s minus the number of ')'s. A string is valid if its balance is 0, plus every prefix has non-negative balance. 
      2. N.B. This only works if there's only one type of parenthese, if there are other types of parentheses, e.g. "{}", this solution breaks.
  2. Use stack:
      1. An interesting property about a valid parenthesis expression is that a sub-expression of a valid expression should also be a valid expression. (Not every sub-expression)
      2. Whenever we encounter a matching pair of parenthesis in the expression, we simply remove it from the expression, and since this is a valid expression, we would be left with an empty string in the end.



4. Problems
    1. [LC921. Minimum Add to Make Parentheses Valid][LC921. Minimum Add to Make Parentheses Valid]
    
5. Resources
[LC921. Minimum Add to Make Parentheses Valid]: https://leetcode.com/problems/minimum-add-to-make-parentheses-valid/
[LC22. Generate Parentheses]: https://leetcode.com/problems/generate-parentheses/





