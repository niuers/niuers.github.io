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
  1. [Keep track of the balance of the string][LC921. Minimum Add to Make Parentheses Valid]: 
      1. The parentheses in a string are balanced if and only if these 2 conditions are met:
        * There are the same number of `(` and `)` in the string.
        * Scanning through the string from left to right and counting how many `(` and `)` there are so far, there should never be a time where there are more `)` than `(`. We call `count("(") - count(")")` the balance of the string.
        * A string is valid if its balance is `0`, plus every prefix has non-negative balance. 
        * Here's a simple pseudocode algorithm that checks for these conditions by scanning through the string and incrementing balance each time it sees a "(", and decrementing each time it sees ")". If at any point the balance is negative, which can only happen if we've seen more ")" than "(", then it returns false. If we get to the end, then it returns true only if the balance is 0, which means we've seen the same number of "(" as ")".
        * remembering that each ")" was paired with the closest "(" that isn't already paired
        * To remove invalid `(`, we need scan backwards from right to left
          * For a given "(" to be valid, there needs to be more ")" than "(" after it in s (if not, there won't be a ")" leftover for it). If this is true for all "(" in s, then s would be valid.
          * When we remove a "(", all other "(" to the left see their ratio of ")" to "(" go up (in other words, they have less others to compete for the ")" with).
          * So by removing balance "(" from the right, every other "(" now has balance less "(" after it, which is the biggest improvement in the ratios we could have possibly got. If any "(" was still not valid after this, then that would mean s had invalid ")" at the start (which it didn't, because it had all of those removed already).
          * Therefore, this has to be a valid solution.
      2. Given `S` composed of only `()`, Let `left` records the number of `(` we need to add on the left of `S`. Let `right` records the number of `)` we need to add on the right of `S`, which equals to the number of current opened parentheses.
        * Loop char `c` in the string `S`: `if c == '('`, we increment `right`, `if c == ')'`, we decrement `right`.
        * When `right` is already `0`, we increment `left`
        * The total balance is `left + right`
      3. The key fact is that, given a valid parenthetical string, we can pick any `)` and move it all the way to the right end, or any `(` and move it all the way to the left end, without invalidating the string. So given a fewest-additions answer, we can take the parentheses we added and move them to the ends, for an equally valid answer. The proof of this fact is by induction.
      4. N.B. This only works if there's only one type of parenthese, if there are other types of parentheses, e.g. "{}", this solution breaks.
      5. Template
      ```
      left, right = 0, 0
      for c in s:
          if right == 0 and c == ')':
              left += 1
          else:
              right += 1 if c == '(' else -1
      return left + right      
      ```
      6. Scan the string left to right, then right to left
        * When scan from right to left, note that we need reset the counts whenever left > right, similary when we scan from left to right, we reset the counts when right > left.
        * There are only three cases for a string:
          * '(' are more than ')'
          * '(' are less than ')'
          * '(' and ')' are the same
          * Now, when you scan from left to right, you can only find the correct maxLength for cases 2 and 3, because if it is case 1, where '(' are more than ')' (e.g., "((()"), then left is always greater than right and maxLength does not have the chance to be updated.
          * Similarly, when you scan from right to left, you can only find the maxLength for cases 1 and 3.
          * Therefore, a two-pass scan covers all the cases and is guaranteed to find the correct maxLength

  2. Use stack:
      1. An interesting property about a valid parenthesis expression is that a sub-expression of a valid expression should also be a valid expression. (Not every sub-expression)
      2. Whenever we encounter a matching pair of parenthesis in the expression, we simply remove it from the expression, and since this is a valid expression, we would be left with an empty string in the end.

4. [Count the number of invalid `(` and `)`][LC301. Remove Invalid Parentheses]
  ```
  left = 0
  right = 0

  # First, we find out the number of misplaced left and right parentheses.
  for char in s:

      # Simply record the left one.
      if char == '(':
          left += 1
      elif char == ')':
          # If we don't have a matching left, then this is a misplaced right, record it.
          right = right + 1 if left == 0 else right

          # Decrement count of left parentheses because we have found a right
          # which CAN be a matching one for a left.
          left = left - 1 if left > 0 else left  
  ```


5. Problems
    1. [LC921. Minimum Add to Make Parentheses Valid][LC921. Minimum Add to Make Parentheses Valid]
    2. [LC32. Longest Valid Parentheses][LC32. Longest Valid Parentheses]
    
6. Resources
[LC921. Minimum Add to Make Parentheses Valid]: https://leetcode.com/problems/minimum-add-to-make-parentheses-valid/
[LC22. Generate Parentheses]: https://leetcode.com/problems/generate-parentheses/
[LC921. Minimum Add to Make Parentheses Valid]: https://leetcode.com/problems/minimum-add-to-make-parentheses-valid/
[LC32. Longest Valid Parentheses]: https://leetcode.com/problems/longest-valid-parentheses/
[LC301. Remove Invalid Parentheses]: https://leetcode.com/problems/remove-invalid-parentheses/



