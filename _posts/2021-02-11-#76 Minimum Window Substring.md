---
title: "76. Minimum Window Substring"
date: 2021-02-11
categories:
  - blog
tags:
  - algorithm
  - leetcode
  - sliding window
---

1. Experience:
    1. I can easily write out the brutal force solution. 
    2. I also figured out that I can increase performance by using some thing like 'sliding window' (didn't realize it's a sliding window problem until I saw the solution)
    3. However, I struggled a lot in implementation. There are probably several reasons:
        * I tried to pre-optimize the solution by always jumping to the character that's in the `t` string. But I did this without first removing the unnecessary characters in `s` string. This seems to complicate the algorithm a lot. I have to check if a char is in the `t` each time. And there are corners cases like when there's one 1 or 2 chars in the `s` string, and one of them is the `t` string.
        * I struggled a lot in the order of actions when I should move left pointer or right pointer. Especially when it's coupled with corner cases. I should have written out the process first before implementing it. 
        * Each time I compare all the characters in the `t` to check if the current substring is a valid one, this still counts as `O(n)` because the number of English letters are fixed (26*2). However, this is slower compared to the solution where they optimized using the number of unique chars matched. I thought about using this as well, but didn't have the energy to implement this as I spent lot of time trying to make the algo work first. 
        * Turns out it's easier to just move left and right by 1 each time. 

2. How did I get the solution? 


3. Different solutions


4. Mistakes

5. Problem Type
    * Sliding window
6. Similar Problems



7. Template



Resources:
* [76. Minimum Window Substring][LeetCode Link]

[LeetCode Link]: https://leetcode.com/problems/minimum-window-substring/