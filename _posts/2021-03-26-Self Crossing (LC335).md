---
title: "Self Crossing (LC335)"
date: 2021-03-26
categories:
  - blog
tags:
  - algorithm
  - leetcode
---

1. Experience:
    1. I wrote a brutal force solution for this problem first. Basically when I have a new segment, I check it against all previous segments and see if there's any crossing.
    2. This is `O(n^2)` and I have to save `O(n)` line segments. The program is kind of messy because it's not so straight forward to determine if two segments are crossing each other. 
    

2. How did I or Other people get the solution? 


3. Different solutions
    1. Other people did it in `O(n)`, where they just deal with 3 different cases that current segment can cross one of the previous segments. Very smart!

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
* [335. Self Crossing][LeetCode Link]


[LeetCode Link]: https://leetcode.com/problems/self-crossing/