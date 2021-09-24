---
title: "Array Problems"
date: 2021-07-18
categories:
  - blog
tags:
  - algorithm
  - array
  - summary
---

1. Find the next greater number in an array
    1. Use stack
    2. Related problems:
        * [LC503 Next Greater Element II][LC503. Next Greater Element II]

2. Two-Sums/Three-Sums
    1. Two Sums: Use hash table to check on the difference. `O(n)`
    2. Two Sums with sorted array: Use two pointers. `O(n)`
    3. Two Sum less than K: You can sort the array first and use two pointers (`O(nlogn)`). If the range of values in the input array `m` is small, you use count sort, the time complexity can be reduced to `O(n+m)`.
    3. Three Sums:
        1. Given that the order of elements doesn't matter, you can sort the input array first to avoid duplicate results (It's important to skip a value if it's the same as previous value in all loops to avoid duplicates). If sort is not allowed, use a set to remove duplicates. `O(n^2)`
        2. You can then re-use one of the solutions for two-sum while holding one of the three numbers fixed `O(n^2)`
    4. 3Sum Closest
        1. sort the array first, then use two pointer to achieve `O(n^2)` solution
        2. Use binary search by fixing first two numbers and search for the third number `O(n^2logn)`
    5. 4Sum and kSum
        1. We can use recursion for kSum problems.
        2. In the case that the sum equals to target value, we can move just one side, e.g. left pointer and check for duplicate while moving it. We don't have to move both left, right pointers at the same time here.
    6. Maximum Size Subarray Sum Equals k
        1. If we look at the prefix sum, a subarray that sums to `k` is equivalent to the subtraction of two prefix sums equals to `k`. If we pre-compute the prefix sum, we can use the concept of two sums (hash set) to find out the index where prefix sum subtracts to `k`
    7. Related problems
        * [LC1. Two Sums][LC1. Two Sums]
        * [LC16. 3Sum Closest][LC16. 3Sum Closest]
        * [LC15. 3Sum][LC15. 3Sum]
        * [LC259. 3Sum Smaller][LC259. 3Sum Smaller]
        * [LC167. Two Sum II - Input array is sorted][LC167. Two Sum II - Input array is sorted]
        * [LC18. 4Sum][LC18. 4Sum]
        * [LC1099. Two Sum Less Than K][1099. Two Sum Less Than K]
        * [LC325. Maximum Size Subarray Sum Equals k][LC325. Maximum Size Subarray Sum Equals k]
    

3. Longest Substring Without Repeating Characters
    1. Use sliding window to avoid checking each substring
    2. Related problems
        * [LC3. Longest Substring Without Repeating Characters][LC3. Longest Substring Without Repeating Characters]

4. Container with Most water
    1. It's similar to find the maximum area between two indices with elements as heights in the array.
        * If we list all the possible combinations of the areas (`O(n^2)`), we see that once we fix two vertical lines, it's only possible to increase the area by moving from the shorter line. Any move from the longer line will decrease the area.
        * This basically starts with some area and tries to see how to optimize it by keeping one edge fixed.
    2. Related Problems
        * [LC11. Container With Most Water][LC11. Container With Most Water]


5. Rotated array problems
    1. If a sorted array is shifted, if you take the middle, always one side will be sorted. Take the recursion according to that rule.
    2. Find a target in a rotated array with unique numbers
        1. Solution 1 (Two passes): Find the index of the smallest number first, then use it to choose which part of the array to search for the target. `O(logn)`
        2. Solution 2 (One pass): `O(logn)`.
            * For each pivot (mid) element, we need to check if it's in a non-rotated part or not by comparing it with the first element. If it's larger than the first element, then [left, pivot] is non-rotated, else, [pivot, right] is non-rotated.
            * Then we compare target with pivot to move the end points
        3. Solution 3: `O(logn)`. When the mid value and target value are not on the same non-rotated part, we set the mid value to INF or -INF correspondingly and reset the end points accordingly. 
    3. Find a target in a rotated array that may contain duplicate numbers
        1. The catch: if `arr[mid]` equals `arr[start]`, then we know that `arr[mid]` might belong to both First and Second parts and hence we cannot find the relative position of target from it.
        2. In this case, we have no option but to move to next search space iteratively (e.g. increase left by 1). Hence, there are certain search spaces that allow a binary search, and some search spaces that don't.
            * Alternatively, we can call the function recursively on two parts of the array separately.
        3. Time complexity : `O(N)` worst case, `O(logN)` best case, where `N` is the length of the input array.
    4. Find the minimum value in the array
        1. We can find the inflection point, when either of the two conditions is satisfied:
            * `nums[mid] > nums[mid + 1]` Hence, `mid+1` is the smallest.
            * `nums[mid - 1] > nums[mid]` Hence, `mid` is the smallest.
    5. Related problems
        * [LC 33. Search in Rotated Sorted Array][LC 33. Search in Rotated Sorted Array]
        * [LC81. Search in Rotated Sorted Array II][LC81. Search in Rotated Sorted Array II]
        * [LC153. Find Minimum in Rotated Sorted Array][LC153. Find Minimum in Rotated Sorted Array]
        * [LC153. Find Minimum in Rotated Sorted Array][LC153. Find Minimum in Rotated Sorted Array]


6. Find First and Last Position of Element in Sorted Array
    1. Basically we need to implement python's `bisect_left` and `bisect_right`
    2. Problems
        * [LC34. Find First and Last Position of Element in Sorted Array][LC34. Find First and Last Position of Element in Sorted Array]

7. Find the maximum/minimum sum of subarray
    1. As expected, any subarray whose sum is positive is worth keeping. Let's start with an empty array, and iterate through the input, adding numbers to our array as we go along. Whenever the sum of the array is negative, we know the entire array is not worth keeping, so we'll reset it back to an empty array. However, we don't actually need to build the subarray, we can just keep an integer variable current_subarray and add the values of each element there. When it becomes negative, we reset it to 0 (an empty array).
    2. Dynamic programming: `O(N)`
    3. Divide and Conquer: `O(NlogN)`
    4. [Kadane's Algorithm Explained][Kadane's Algorithm Explained]: it solves the problem of finding the maximum subarray sum in a one-dimensional array
        * At each index, we have two choices: either start at the current index or add the current element to the previous sum.
        * And since we want the maximum subarray sum, we add the current element to the maximum of `0` and previous sum (zero here denotes that we’re starting anew from the current element).
        * Let’s take an array `dp[]` where each `dp[i]` denotes maximum subarray sum ending at index `i` (including `i`). We have `dp[i] = max(dp[i-1], 0) + nums[i]`.
    4. Problems
        * [LC53. Maximum Subarray][LC53. Maximum Subarray]
        * [LC152. Maximum Product Subarray][LC152. Maximum Product Subarray]

8. Jump to the end of array game
    1. Dynamic programming gives `O(N^2)`
    2. If we use greedy method, we can reduce to `O(N)`
    3. Problems
        * [LC55. Jump Game][LC55. Jump Game]

9. Merge Sorted Arrays
    1. Whenever you're trying to solve an array problem in-place, always consider the possibility of iterating backwards instead of forwards through the array. It can completely change the problem, and make it a lot easier.
    2. Problems
        * [LC88. Merge Sorted Array][LC88. Merge Sorted Array]

10. Compute the maximum profit
    1. Only 1 buy and 1 sell transactions allowed
        * Record the current minimum price and update the maximum profit while looping through the array
    2. Multiple buy and sell transactions allowed
        * Peak Valley approach (draw picture): 
            * The points of interest are the consecutive valleys and peaks. The key point is we need to consider **every peak immediately following a valley** to maximize the profit. In case we skip one of the peaks (trying to obtain more profit), we will end up losing the profit over one of the transactions leading to an overall lesser profit.
            * Find consecutive peaks and valleys, and use them to compute the profit
        * We can directly keep on adding the difference between the consecutive numbers of the array if the second number is larger than the first one, and at the total sum we obtain will be the maximum profit
    3. Multiple buy/sell transactions with cool down
        * State Machine + Dynamic Programming `O(n)`
            * we will treat the problem as a game, and the trader as an agent in the game. The agent can take actions that lead to gain or lose of game points (i.e. profits). And the goal of the game for the agent is to gain the maximal points.
            * Now if we chain up each state at each price point, it would form a graph where each path that starts from the initial price point and ends at the last price point represents a combination of transactions that the agent could perform through out the game.
            * In each node of graph, we also indicate the maximal profits that the agent has gained so far in each state of each step.
            * States: held, sold, reset
            * Actions: sell, buy, reset
        * Dynamic Programming `O(n^2)`
    4. [A consistent way to solve such problems][Most consistent ways of dealing with the series of stock problems]
        * Let `T[i][k]` be the maximum profit that could be gained at the end of the `i-th` day with at most `k` transactions.
        * How many options do we have on the `i-th` day? The answer is three: `buy`, `sell`, `rest`.
            * However, the `buy/sell` actions depend on how many stocks we have beforehand
            * So we should put 3rd state into the matrix `T[i][k][0] and T[i][k][1]` indicating we have a stock or not after taking an action
    5. Problems
        * [LC121. Best Time to Buy and Sell Stock][LC121. Best Time to Buy and Sell Stock]


11. [LC128. Longest Consecutive Sequence][LC128. Longest Consecutive Sequence]

12. [Find the duplicate][LC287. Find the Duplicate Number]
    1. use hash set:  `O(n)` in time, `O(n)` in space
    2. Set elements to negative:  `O(n)` in time, `O(1)` in space
        * It modifies input array
    3. Recursion-Swap elements to corresponding index: `O(n)` in time, `O(n)` in space
    4. Swap elements to corresponding index: `O(n)` in time, `O(1)` in space
        * It modifies input array
    5. binary search: `O(nlogn)` in time, `O(1)` in space
        * the duplicate number will have a count of numbers less than or equal to itself, that is greater than itself. Hence, the smallest number that satisfies this property is the duplicate number. Since `count(N) >= count(N-1)`, countcount must be monotonically increasing.
    6. sum of set bits:  `O(nlogn)` in time, `O(1)` in space
        * Let's look at each of these numbers in binary and count the number of times 1 is seen at each bit position. By iterating over each bit, and comparing the base (without duplicate from `1` to `n`) to the current, we were able to construct the duplicate number bit by bit.
        * So how does this work if the duplicate number appears more than twice? In that case, think of it as simply replacing the missing numbers with the duplicate number, effectively reducing the count of 1's corresponding to the missing numbers and adding 1's associated with the duplicate number - so the algorithm remains intact, since the count of 1's will be even more pronounced in favor of the duplicate number. If we consider just the positive counts it's the duplicate.
        * A key observation is that if the array had `n` elements instead of `n + 1` (where each element is in the range `[1,n]`), this solution would not work. The extra number ensures that bit counts at the right positions are always added and never taken away from the base_count.
    7. Floyd's Tortoise and Hare (Cycle Detection) : `O(n)` in time, `O(1)` in space
        * The cycle appears because nums contains duplicates. The duplicate node is a cycle entrance.
    8. sort

13. [Wiggle Sort][LC324. Wiggle Sort II]
    1. [Partition][Summary of the various solutions to Wiggle Sort for your reference]: this will partition the array (with a total of `n` elements) into two groups which will be called `S` and `L`, respectively. The `S` group will have `m=int((n+1)/2)` elements and the `L` group contains the rest. Also all elements in the `L` group is no less than those in the `S` group. (Note for this partition, `S` and `L` group will have the same number of elements as the even group and odd group, respectively. And the size of `L` group is no more than that of `S` group.)
    2. Placement: if all elements in the `L` group is greater than those in the `S` group, we can simply place elements in the `L` group at odd indices (thus form the odd group) and those in the `S` group at even indices (form the even group). The tricky case is when there are overlapping (or equal) elements between the two groups.
        * Let `i` be the index of an element before placement and `j` the index after, for ascending order, we have:
        ```
        j = 2 * (m - 1 - i) if i < m
        j = 2 * (n - 1 - i) + 1 if i >= m
        ```
    3. First we prove that if the array can be "wiggly-sorted", the total number of such overlapping elements is no more than the size of the `S` group, which is `m`. 
    4. Second we show that if we arrange these overlapping elements in such a way that they will occupy the smallest even indices possible if they come from the `S` group and will take the largest odd indices possible if they are from the `L` group, then none of them will be neighbors of others. 
    5. We put the numbers larger than median to the left, and numbers smaller than median to the right, then put the medians to the left over positions. 
        * Use quickselect to find the median first
    6. N.B. once we find the median, the right/left sides of it can still have the same value of median, and they may not be arranged toward the median, so we need another `O(n)` to move all numbers larger than the median to the right, and all numbers smaller than the median to the left, such that the medians occupy the middle part in a continguous subarray. Then we put the numbers to their proper positions
            

14. Classical K-th Problem
    1. Sort the array and select the first k-th elements. `O(NlogN)`, doesn't allow on-line process
    2. Put the elements into a max-heap of size k, `O(NlogK)`, can be applied to on-line process
    3. Use quick-select, average `O(N)`, worst case `O(N^2)`
    4. Problems
        * [LC973. K Closest Points to Origin][LC973. K Closest Points to Origin]


[LC503. Next Greater Element II]: https://leetcode.com/problems/next-greater-element-ii/
[LC1. Two Sums]: https://leetcode.com/problems/two-sum/
[LC3. Longest Substring Without Repeating Characters]: https://leetcode.com/problems/longest-substring-without-repeating-characters/
[LC11. Container With Most Water]: https://leetcode.com/problems/container-with-most-water/
[LC16. 3Sum Closest]: https://leetcode.com/problems/3sum-closest/
[LC15. 3Sum]: https://leetcode.com/problems/3sum/
[LC259. 3Sum Smaller]: https://leetcode.com/problems/3sum-smaller/
[LC167. Two Sum II - Input array is sorted]: https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/
[LC18. 4Sum]: https://leetcode.com/problems/4sum/  
[LC1099. Two Sum Less Than K]: https://leetcode.com/problems/two-sum-less-than-k/
[LC33. Search in Rotated Sorted Array]: https://leetcode.com/problems/search-in-rotated-sorted-array/
[LC81. Search in Rotated Sorted Array II]: https://leetcode.com/problems/search-in-rotated-sorted-array-ii/
[LC153. Find Minimum in Rotated Sorted Array]: https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/
[LC34. Find First and Last Position of Element in Sorted Array]: https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/
[LC53. Maximum Subarray]: https://leetcode.com/problems/maximum-subarray/
[LC55. Jump Game]: https://leetcode.com/problems/jump-game/
[LC88. Merge Sorted Array]: https://leetcode.com/problems/merge-sorted-array/
[LC121. Best Time to Buy and Sell Stock]: https://leetcode.com/problems/best-time-to-buy-and-sell-stock/
[1D Kadane Algorithm]: https://en.wikipedia.org/wiki/Maximum_subarray_problem
[Kadane's Algorithm Explained]: https://hackernoon.com/kadanes-algorithm-explained-50316f4fd8a6
[LC128. Longest Consecutive Sequence]: https://leetcode.com/problems/longest-consecutive-sequence/
[LC152. Maximum Product Subarray]: https://leetcode.com/problems/maximum-product-subarray/
[LC153. Find Minimum in Rotated Sorted Array]: https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/
[LC287. Find the Duplicate Number]: https://leetcode.com/problems/find-the-duplicate-number/
[Most consistent ways of dealing with the series of stock problems]: https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-transaction-fee/discuss/108870/most-consistent-ways-of-dealing-with-the-series-of-stock-problems
[LC325. Maximum Size Subarray Sum Equals k]: https://leetcode.com/problems/maximum-size-subarray-sum-equals-k/
[LC324. Wiggle Sort II]: https://leetcode.com/problems/wiggle-sort-ii/
[Summary of the various solutions to Wiggle Sort for your reference]: https://leetcode.com/problems/wiggle-sort-ii/discuss/77684/Summary-of-the-various-solutions-to-Wiggle-Sort-for-your-reference
[LC973. K Closest Points to Origin]: https://leetcode.com/problems/k-closest-points-to-origin/