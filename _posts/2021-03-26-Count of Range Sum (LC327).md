---
title: "Count of Range Sum (LC327)"
date: 2021-03-26
categories:
  - blog
tags:
  - algorithm
  - leetcode
  - Divide and Conquer
  - Binary Search
  - Binary Indexed Tree
  - Segment Tree
---

1. Experience:
    1. I first implemented a brutal force solution, `O(n^2)` in complexity. It got TLE.
    2. I couldn't think about a better way to solve the problem, so I looked at the hints. They are talking about binary search, sort, binary indexed tree, segment tree and divide and conquer. 
        * I kind of understand that we can use segment tree to improve the performance, but sure how though because I am not familar with the data structure.
    3. I still didn't know how to do divide and conquer. Don't we still need to use `O(n^2)` to merge the two sub arrays? 
    4. I read the discussion, it turned out that we don't need worry about the order of the prefix sums in the second subarray, that's where we can use `O(n(logn)^2)` algorithm.
    5. I implemented it with success.
    

2. How did I or Other people get the solution? 


3. Different solutions


4. Mistakes

5. Problem Type
    
6. Similar Problems

7. Template

8. I understand the solution, but HOW do I think to GET there myself?
    1. Where could you improve?
        * When the problem hints that we should improve the performance of `O(n^2)`. I naturally thought about `O(nlogn)` and `O(n)`. The latter looks less feasible, so I focused on `O(nlogn)`. 
        * However, I didn't come up with sort and binary search. 
        * Next time, when I think about `O(nlog(n))` solution, I should think about sort and binary search.
    2. What questions should I ask myself so that I push myself closer to the solution? 
    3. What conclusions did I reach that I dropped some idea for the other?
    4. How can I reach this conclusion faster ?
    



Resources:
* [327. Count of Range Sum][LeetCode Link]


[LeetCode Link]: https://leetcode.com/problems/count-of-range-sum/