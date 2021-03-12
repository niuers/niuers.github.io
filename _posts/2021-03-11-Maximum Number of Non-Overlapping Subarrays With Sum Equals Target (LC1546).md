---
title: "Maximum Number of Non-Overlapping Subarrays With Sum Equals Target (LC1546)"
date: 2021-03-11
categories:
  - blog
tags:
  - algorithm
  - leetcode
  - dynamic programming
---

1. Experience:
    1. I didn't have much clue at first. There can be many subarrays and I have to find out the maximum number of non-overlap subarrays?
    2. I split the problem into two steps: 
        1. I first compute out all the subarray sums. This is a matrix, with only the right half used. While I am computing the subarray sums, I put all the subarrays with target sum into a separate array. This takes `O(n^2)` time.
        2. Then I started to tackle the problem of how to find maximum non-overlap subarrays. 
        3. I tried to use dynamic programming on the second part. I setup an array `dp` with `dp[i]` to represent the maximum number of non-overlap subarrays ending at index `i`. Then I loop `i` from `0 to n`, and for each index, I check if the start position of `i` is later than the ending position for the segments before `i`. And I update the counts of subarrays by adding 1.
        4. So this takes `O(n^2)`, it got TLE.
        5. I noticed that I can use the cumulative sums to compute the subarray sums. So I pull out the calculation of cumulative sums and use it to calculate the subarray sums. Still the overall complexity is `O(n^2)`, TLE.
    3. I had to read the hints and solutions for the problem. The new information I got is that I can use greedy method here. So once I find a subarray at index `i`, when I go to the next index, I don't have to compute all the subarray sums from indexes before `i` to current index because that will not increase the number of non-overlap subarrays. So it's not optimal to consider the indexes before `i` once we have found one at `i`. The new solution can just restart the search from `i+1`. 
        1. So I used `O(n)` to find out the cumulative sums for the array.
        2. Then I tried to find the maximum number of non-overlapping subarrays using greedy method. Since in greedy method, I don't need memorize the counts from previous indexes, I don't need an array for dynamic programming here. 
        3. The trick here is how to iterate through the dynamic table (although we don't use a table in implementation, it helps to visualize the process using a table on paper). 
        4. Basically, at index `i`, we want to make sure we have checked all the subarrays before and at index `i`. However, this solution is still `O(n^2)`, and TLE. 
        5. The real trick is to use a hashset when we check whether a sum equals to the target. Notice that we are always comparing `sums[i]-sums[j]` with target for `j=0,1,...,i` (well you need reset the starting value for `j` once we find a valid subarray). It's equivalent to compare `sums[i] - target` with `sums[j]` and the `sums[j]` are the values we computed out already. So if we keep them in a set, it'll be `O(1)` operation to check.
        6. In the end, we have `O(n)` solution.


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
* [1546. Maximum Number of Non-Overlapping Subarrays With Sum Equals Target][LeetCode Link]


[LeetCode Link]: https://leetcode.com/problems/maximum-number-of-non-overlapping-subarrays-with-sum-equals-target/