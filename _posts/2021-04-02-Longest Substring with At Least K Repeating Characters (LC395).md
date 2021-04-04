---
title: "Longest Substring with At Least K Repeating Characters (LC395)"
date: 2021-04-02
categories:
  - blog
tags:
  - algorithm
  - leetcode
  - Divide and Conquer
  - Sliding Window
---

1. Experience:
    1. At the beginning, I don't have much clue how to solve this problem. I thought it's related to dynamic programming. 
    2. I tried to build the dynamic programming table, and see how can I transit from one substring to the next. It didn't get me anywhere. 
    3. Later, I tried to write out the brutal force solution first. Loop through each possible substrings, and counter the number of characters and find the maximum length of such string.
    4. It somehow gave me some idea, I realized that if a character has less than `k` counts in the string, then the character can't be in the substring that satisfies the requirement. This means I can remove it from the counting.
    5. It gave me the idea to do divide and conquer. Where I started with the full string, and find the character with the smallest count, if it's larger than `k`, we are done. Otherwise, I find the position of the character, and split the string into two parts, and call the function recursively to find which one has the solution.
    6. This passes the tests, and I thought a better way is to try split the string each time at the middle if possible, so I store the indices of each character in the map, and pick the middle indice from the list. This improves the performance a lot. But the worst time complexity is still `O(n^2)`.

2. How did I or Other people get the solution? 


3. Different solutions
    1. The solution is using the sliding window, which takes `O(n)`. The main point is to fix the number of unique character first. This is very hard to think about.

4. Mistakes

5. Problem Type
    
6. Similar Problems

7. Template

8. I understand the solution, but HOW do I think to GET there myself?
    1. Where could you improve?
    2. What questions should I ask myself so that I push myself closer to the solution? 
    3. What conclusions did I reach that I dropped some idea for the other?
    4. How can I reach this conclusion faster ?
    



Resources:
* [395. Longest Substring with At Least K Repeating Characters][LeetCode Link]


[LeetCode Link]: https://leetcode.com/problems/longest-substring-with-at-least-k-repeating-characters/