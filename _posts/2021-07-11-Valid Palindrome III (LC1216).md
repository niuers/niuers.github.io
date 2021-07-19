---
title: "Valid Palindrome III (LC1216)"
date: 2021-07-11
categories:
  - blog
tags:
  - algorithm
  - leetcode
  - dynamic programming
---

1. Experience:
    1. At the beginning, I was trying to use recursive method to solve it. In the recursive call, I tried to remove each charater in the current string, and recursively call the new string to see if it's a valid palindrome. This definitely takes too long to run, and I got TLE.
    2. later, I figured out that for the first character, I can do two things: 
        1. Remove the character and check if the rest is a valid palindrome
        2. Leave the character, then it means that there's a matching character in the end, I run through the end until I find the matching character, and check how many characters have been removed. If it's less than the required, I recursively call the function on the string in the middle. Otherwise, it's False in this case.
        3. If either of the above two cases return True, I can return True for the current string. 
        4. If I return earlier given that the first case (or second case) is true, I can pass the test cases. However, the rank is very low.
    3. I then realized that I can use a 3D dynamic programming table to solve this as well. `d[i][j][k]`, where `d[i][j]` is the 2D table when `k=some value`. This 2D table has a size of `NxN` where `N` is the size of the string. `d[i][j]=1` means string `s[i:j]` is a valid palindrome with less or equal to `k` removals. This will take `O(n^3)` time complexity.

2. How did I or Other people get the solution? 

3. Different solutions
    1. The solution changes the problem into "how many removals needed to make the rest string a palindrome such that the total remove is less or equal to k?"
    2. This makes it easier to reason about the process. So it uses two pointers to go from both ends, and count for difference cases. 
4. Mistakes
    1. The thing I missed is that I didn't realize that I can work from both ends. This reduces 1 dimension from the problem.

5. Problem Type


  
6. Similar Problems

7. Template

8. I understand the solution, but HOW do I think to GET there myself?
    1. Where could you improve?
    2. What questions should I ask myself so that I push myself closer to the solution? 
    3. What conclusions did I reach that I dropped some idea for the other?
    4. How can I reach this conclusion faster ?
    



Resources:
* [LC1216. Valid Palindrome III][LeetCode Link]

[LeetCode Link]: https://leetcode.com/problems/valid-palindrome-iii/