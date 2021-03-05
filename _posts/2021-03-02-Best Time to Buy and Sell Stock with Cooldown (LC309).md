---
title: "Best Time to Buy and Sell Stock with Cooldown (LC309)"
date: 2021-03-02
categories:
  - blog
tags:
  - algorithm
  - leetcode
  - dynamic programming
  - state machine
---

1. Experience:
    1. I couldn't solve this problem.
    2. I was trying to check different cases to compare the valley, peak in the price history and see if I can find some pattern. It's very complicate since we have a cool down period, I have to consider the case whether should I sell in the last peak, or the day before last peak, and buy in the day right after last peak, etc. Especially when a valley is followed immediately after a peak, giving no cool down.
    3. I had to read the solution and found they are using dynamic programming, which is straightforward.
    4. The state machine solution is not intuitive to me. 

2. How did I or Other people get the solution? 


3. Different solutions




4. Mistakes

5. Problem Type
    * Dynamic Programming
    * State Machine

6. Similar Problems
  1. 


7. Template



Resources:
* [309. Best Time to Buy and Sell Stock with Cooldown][LeetCode Link]


[LeetCode Link]: https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/