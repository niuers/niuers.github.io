---
title: "Burst Ballons (LC312)"
date: 2021-03-24
categories:
  - blog
tags:
  - algorithm
  - leetcode
  - dynamic programming
---

1. Experience:
    1. I quickly got the recursive solution for this problem. To solve the problem, I tried to burst the ballon `i` first, then the recursive function shall work with the new array without entry `i`. To get the maximum coins, I need to try the `i` from `1 to n-1` and choose the maximum coins among them.
        * This is of course very time consuming. I had to choose from `N` ballons at the beginning, then I had to choose from `N-1` ballons next, etc. So the time complexity is `N!`.
        * I tried to list out all possible combinations for three and four ballons in a tree structure. They do share common combinations.
        * I later put a cache into the code, where I used the string representation of the array as hash key. This improves the performance a bit, but still got TLE pretty soon.
    2. I worked out some examples here
        * I noticed that we can remove `0` first, otherwise if we remove the numbers beside `0`, we must get coins less than maximum since `0` contriute nothing to the coins.
    3. I thought I found a rule on which ballon to burst first
        * I used example `[3,1,5,8]` and `[7,9,8,7,5]`. I noticed that for a given ballon, if I compute the product of the two numbers beside the ballon, and it seems we should pick the ballon with the largest such product. If there are two ballons that having the same product, we should pick the ballon with the smaller number itself. 
        * This can be easily proved wrong using example `[3,7,2]`.
        * I tried to find out the pattern for three ballons without any success.
    4.   
    5. I checked the hint, it says divide and conquer, dynamic programming
        * I came back to dyanmic programming, trying to establish the table. 
        * The thing blocking me is that I don't know how to move from one table entry to the next. When I burst a ballon, if the ballon is in the middle, I have to connect the ballons before and after it to form a new array. This however, destroies the original dynamic table. I mean, I can't re-use the quantities computed from previous step.
        * Then I was thinking about how to use divide and conquer, it didn't result in anything that's usable for the same reason above. I can't just divide them.
    

2. How did I or Other people get the solution? 
    1. There are two important points to solve this problem.
    2. Firstly, instead of thinking about which ballon to burst **first**, we should think about which ballon to burst **last**. 
        * The benefit is that we don't have to work with a new array, instead we work with a subarray becase there's a boundary established by the last burst ballon. 
    3. Secondly, the entries in dynamic table `dp[i][j]` represents the maximum coin by bursting ballons between `i` and `j`, where `i,j` are excluded.
        * This way, we built a wall to stop the calculations.
        * Otherwise, when we are computing the coins by bursting the boundary ballons, we have to use the ballon information on its right or left side, so to compute the coin. 

3. Different solutions


4. Mistakes

5. Problem Type
    
6. Similar Problems

7. Template

8. I understand the solution, but HOW do I think to GET there myself?
    1. Where could you improve?
        * This is a problem where the action destroies original data strucutre. It makes it impossible to reuse previously computed results.
        * I should try on both directions: forward and backward
        * When build up the dynamic table entry, `dp[i][j]`, try to make all the information availabe to compute the entry. That is, the array from `a[i:j+1]` plus information of other table entries should be enough to compute. If not, try modify the definition of table entry to accomodate this.
    2. What questions should I ask myself so that I push myself closer to the solution? 
        * What is the last ballon to burst?
    3. What conclusions did I reach that I dropped some idea for the other?
        * 
    4. How can I reach this conclusion faster ?
    



Resources:
* [312. Burst Ballons][LeetCode Link]


[LeetCode Link]: https://leetcode.com/problems/burst-balloons/