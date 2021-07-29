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
    6. Related problems
        * [LC1. Two Sums][LC1. Two Sums]
        * [LC16. 3Sum Closest][LC16. 3Sum Closest]
        * [LC15. 3Sum][LC15. 3Sum]
        * [LC259. 3Sum Smaller][LC259. 3Sum Smaller]
        * [LC167. Two Sum II - Input array is sorted][LC167. Two Sum II - Input array is sorted]
        * [LC18. 4Sum][LC18. 4Sum]
        * [LC1099. Two Sum Less Than K][1099. Two Sum Less Than K]
    

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
    4. Related problems
        * [LC 33. Search in Rotated Sorted Array][LC 33. Search in Rotated Sorted Array]
        * [LC81. Search in Rotated Sorted Array II][LC81. Search in Rotated Sorted Array II]
        * [LC153. Find Minimum in Rotated Sorted Array][LC153. Find Minimum in Rotated Sorted Array]


6. Find First and Last Position of Element in Sorted Array
    1. Basically we need to implement python's `bisect_left` and `bisect_right`
    2. Problems
        * [LC34. Find First and Last Position of Element in Sorted Array][LC34. Find First and Last Position of Element in Sorted Array]

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