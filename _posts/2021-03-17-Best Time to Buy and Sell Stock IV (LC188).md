---
title: "Best Time to Buy and Sell Stock IV (LC188)"
date: 2021-03-17
categories:
  - blog
tags:
  - algorithm
  - leetcode
  - dynamic programming
---

1. Experience:
    1. This is really hard problem for me. I couldn't come up with a solution that can be accpeted.
    2. At first, I thought about the maximum profit that can be achieved when we buy on the day `i`.
        * I drew pictures of some cases of the prices, e.g. increase first then decrease, always increasing, always decreasing, flat etc. 
        * If I buy a stock at day `i`, I thought that I'll achieve maximum profit if I sell at the first peak after day `i`. Because there's no cooldown period, I can always buy right after the first peak, and sell at later peak to achieve better profit. e.g. `[1,5,3,9]`, I buy at price `1` and `3` and sell at `5` and `9` to get total profits of `10`, which is higher than buy at `1` and sell at `9`, which has a profit of `8`.
        * Once I have the maximum possible profits for each day, I store them in a priority queue and the top `k` profits are what I need to get the maximum profits with at most `k` transactions.
        * This is totally wrong. When there's a constraint of at most `k` transactions, the case that I always get maximum profit if I see at the first peak doesn't hold. Given the same example as above, if I can only do one transaction, I should buy at `1` and sell at `9`.
    3. As my first solution doesn't work. I started to think about using dynamic programming (since I knew DP works for some other stock trading problems). I tried a 2D dynamic table first, with the prices in row and column dimensions. I use `dp[i][j]` to represent the maximum profit achieveable from day `i` to day `j` with at most `k` transactions.
        * I tried to work out the table using example prices `[1,4,2,7,2,9]`
        * To goto the next stage, i.e. `dp[0][3]`, the maximum profits for prices `[1,4,27]`. If `k=2`, I had to check the maximum profits achieveable by spliting the trasactions in one of the elements of the array, as well as checking the profits made by using `k=1`.
        * In this way, for each day in the original prices array, I had to check for each following day, what's the profit if I sell at that date, then combine with the maximum profits achived through the rest of days (which is recursive here)
    4. The above recursive method definitely costs a lot of time (factorial!). So I thought about other methods:
        * I tried to build a table by combining the prices with number of transactions. 
            * I somehow couldn't find the transition function. I don't know why.
            * After I read some dicussions, I realized that some other people use this table to find out the solution. 
        * I tried to work both forward and backward, couldn't figure out the transition function here.
    5. I implemented the recursive solution. Through trial and error, I realized that for each date, I have to try such recursive thing to find the maximum profits. Clearly, I am getting to TLE.
    6. I realized that when we sell, we only sell at the peaks. So I thought it might help if we only do such recursive calls in all available peaks (as compared to all elements).
    7. I started to write a function to find out all peaks:
        * I drew a set of graphs representing possible changes of prices.
        * There are 3 cases in general: prices go up, prices go down, prices keep constant.
        * Then I drew the cases where there are 1 peak or 1 valley.
        * It's not that straightforward to summarize all the cases here. 
        * I finally get following patterns:
            * I compare slopes before and after to see what cases I am in.
            * If current slope is `<=0`, I update the price to buy with current price
            * If current slope if `>0`, then I update the current peak price (price to sell) with current price
            * If prevous slope is `>0` and current slope is `<=0`, we find a peak, I compute the profit and push the buy price and sell price into an array.
        * I changed the recursive function to use peaks only. Still got TLE. It doesn't help at all.
    8. I had to think about other solutions
        * One thing I thought is to use 3D dynamic table, fix the `k` each time, and use a 2D table to represent the profits going from day `i` to day `j` with exact `k` transactions.
        * It seems to be very complicate to implement. I think the time complexity is `O(kn^3)`. Because at `k=2`, I had to check each split point to see what's the maximum profits. So to populate the table at `k=2`, each element is `O(n)`, and we have `n^2` elements.
        * I couldn't find an explicite formula that simple enough to make the transition.
        * I struggled with the question: What states to save for dynamic table? 
    



2. How did I or Other people get the solution? 
    1. The solution said to use dynamic programming with 3D table. I didn't realize that we can use the status of stock holding at a date to simplify the problem. 
    2. I don't think I can figure out the last state variable (i.e. number of stocks) for the dynamic table. How do one get this? Is there any pattern for such solution? 

3. Different solutions


4. Mistakes
    1. I didn't try to think about how large can `k` go. I tried the case when `k=1`.

5. Problem Type
    
6. Similar Problems

7. Template

8. I understand the solution, but HOW do I think to GET there myself?
    1. Where could you improve?
        * When deal with problems asking something like `at most` or `at least`, I should think about fixing the variable first otherwise it's very hard to think about a transition function.

    2. What questions should I ask myself so that I push myself closer to the solution? 
        * What are possible ranges of `k` as compared to `n`?
        * When you are trying to find out the transition function, think about this:
            * What's the new information?
            * How should I use it to construct transition function?
            * What's the formula for new entry if I don't use it? Will it reduce to previously computed entry?
            * What's the formula for new entry if I use it?
    3. What conclusions did I reach that I dropped some idea for the other? 
    4. How can I reach this conclusion faster ?
    



Resources:
* [188. Best Time to Buy and Sell Stock IV][LeetCode Link]


[LeetCode Link]: https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iv/