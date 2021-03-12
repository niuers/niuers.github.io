---
title: "Best Team With No Conflicts (LC1626)"
date: 2021-03-11
categories:
  - blog
tags:
  - algorithm
  - leetcode
  - dynamic programming
---

1. Experience:
    1. The first time I saw this problem, it seems to be very complicate, there's interaction between age and score. I know that I should sort them out first, but I don't know how to use that information. 
    2. Maybe I should try use sorted array first to get better idea.
    3. Anyway, I didn't do that, I tried to solve with brutal force solution, where I assume that can give me some idea how to solve this problem. 
    4. I wrote a recursive function to solve this, basically loop on each player, and check the maximum score we can obtain without including him. This is exponentially in time complexity and it got TLE quicly.
    5. I might be tired of thinking in the afternoon, I looked into hints and found that one important information is that once we picked a player from sorted array, the later players we picked have to have larger scores.  
    6. This helped a lot here. So I started to implement an `O(n^2)` solution. First use a recursive method, then simplify it using dynamic table.


2. How did I or Other people get the solution? 


3. Different solutions


4. Mistakes

5. Problem Type

6. Similar Problems
  1. 


7. Template

8. I understand the solution, but HOW do I think to GET there myself?
  1. Where could you improve? 
  2. What questions should I ask myself so that I push myself closer to the solution? 
  3. What conclusions did I reach that I dropped some idea for the other? 
  4. How can I reach this conclusion faster ?



Resources:
* [1626. Best Team With No Conflicts][LeetCode Link]


[LeetCode Link]: https://leetcode.com/problems/best-team-with-no-conflicts/