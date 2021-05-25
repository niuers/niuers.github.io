---
title: "Campus Bikes II (LC1066)"
date: 2021-05-25
categories:
  - blog
tags:
  - algorithm
  - leetcode
  - backtracking
---

1. Experience:
    1. At first I tried to sort both workers and bikes by their distances to the origin (`abs(x)+abs(y)`), then for each worker, I use binary search to find the bike that's closest to it. This didn't work out to find the optimal distance.
    2. It turned out to be a backtrack problem, where for each worker, one by one, I have to pair with each bike, and see if it can give us minimum total distance, if not, we backtrack and try the next bike.
    3. This turned out to be difficult for me to implement.
        * What is the state of the problem at each step?
        * Given the state, how do I cache them as a key, such that later stages can reuse the results ?
    4. In the process, we always start from worker `0` to worker `n`, so if workers `0` to `k-1` have occupied `k` bikes, the rest of workers will only find possible bikes in the rest of bikes. These `k` workers can pair with different `k` bikes, for any given combination of `k` bikes though, the `n-k` workers will pair with the same set of `m-k` bikes (which can have combinatorial pairs in total). We can thus have a cache, where the keys are the combination of bikes (that have not been paired with a worker). 
        * For example, if there are 8 workers, 8 bikes. If the first 3 workers are paired with bikes 0,3,5 (note even though the paired workers and bikes are fixed, there are still multiple ways to pair them differently), then we have a bike array like `[10010100]`, the workers `3-7` will pair with bikes `1,2,4,6,7`. We can use the bike array to cache the minimum distance one can obtain by pairing workers `3-7` with bikes `1,2,4,6,7`. Then we can re-use the cache whenever we encounter the same bike array when making combinations of workers `0-2` with bikes `0,3,5`.
        * Note that each bike can be in paired or not paired state, so the total number of different bike arrays is `2^(len(bikes))`. 


2. How did I or Other people get the solution? 

3. Different solutions
    1. dijstra algorithm

4. Mistakes
    1. I tried two ways of implementing backtrack. Suppose our backtrack function is called `f`.
    2. Solution 1: Pass the current total distance as an argument in `f`
        * e.g. `backtrack(worker_id, visited, current_distance)`
        * each time if the current `worker_id == len(workers)`, we compare the `current_distance` with the current minimum distance, if it's smaller, we update the minimum distance.
        * This seems to work. But it breaks when we want to use cache to speed up the program. Suppose we just paired worker `k` with a bike. The `current_distance` is the current total distance pairing workers `0-k` to `k+1` bikes. It's not necessarily the minimum total distance. So instead of caching the minimum total distance for this config, we cache some distance here. 
        * As we can see above, the cached values should be the minimum total distance by pairing workers `k-n` with the rest of bikes. That's why this solution doesn't work here.        
    3. Solution 2: Return the minimum total distance from backtrack function `f`
        * As discussed above this one has clear definition of what we are caching and the usage is straightforward.

5. Problem Type
    
6. Similar Problems

7. Template

8. I understand the solution, but HOW do I think to GET there myself?
    1. Where could you improve?
    2. What questions should I ask myself so that I push myself closer to the solution? 
    3. What conclusions did I reach that I dropped some idea for the other?
    4. How can I reach this conclusion faster ?
    



Resources:
* [1066. Campus Bikes II][LeetCode Link]


[LeetCode Link]: https://leetcode.com/problems/campus-bikes-ii/