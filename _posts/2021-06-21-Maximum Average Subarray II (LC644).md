---
title: "Maximum Average Subarray II (LC644)"
date: 2021-06-21
categories:
  - blog
tags:
  - algorithm
  - leetcode
  - stack
---

1. Experience:
    1. I was able to get the `O(n^2)` solution using prefix sums. However, this is TLE.
    2. I don't know how to solve the problem using a better time complexity. The array is not sorted. 
    3. The solution does binary search on the range of average values. This is tricky. So it searches the average value by specifying the tolerance to 1.0e-5. Each time, it check if there's a subarray that has a average larger than the current value. This check can be completed in `O(n)` time. 
        * It's also interesting that the check applies a minimum of prefix sums. Which doesn't require `O(n^2)` time.

2. How did I or Other people get the solution? 

3. Different solutions

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
* [LC644. Maximum Average Subarray II][LeetCode Link]

[LeetCode Link]: https://leetcode.com/problems/maximum-average-subarray-ii/