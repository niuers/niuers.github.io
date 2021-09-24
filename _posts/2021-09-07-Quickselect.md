---
title: "Quickselect"
date: 2021-09-07
categories:
  - blog
tags:
  - algorithm
  - summary
---

1. [Quickselect (Hoare's selection algorithm)][Quickselect] to find the `k-th` something: kth smallest, kth largest, kth most frequent, kth less frequent, etc.
    1. Average `O(n)` time complexity, `O(N^2)` in worst case
        * In the worst-case of constantly bad chosen pivots, the problem is not divided by half at each step, it becomes just one element less, that leads to `(N^2)` time complexity. It happens, for example, if at each step you choose the pivot not randomly, but take the rightmost element. For the random pivot choice the probability of having such a worst-case is negligibly small.
    2. First one chooses a random pivot, and finds its position in a sorted array in linear time using **partition algorithm**.
        * To implement partition one moves along an array, compares each element with a pivot, and moves all elements smaller than pivot to the left of the pivot.
        * Then we swap the pivot to its correct position
        * N.B. This is in-place select, As an output we have an array where pivot is on its perfect position in the ascending sorted array, all elements on the left of the pivot are smaller than pivot, and all elements on the right of the pivot are larger or equal to pivot. Importantly, This invariant is just for the **partition algorithm**, not for the final `find_kth_element` program, as the elements before or after the `k-th` one can still equal to the `k-th` element.
        * 

    3. Code Template
    ```
    def find_pivot_index(nums, left, right, random_idx):
        pivot = nums[random_idx]
        nums[right], nums[random_idx] = nums[random_idx], nums[right]
        pivot_idx, j = left, right-1
        while pivot_idx <= j:
            if nums[pivot_idx] < pivot:
                pivot_idx += 1
            else:
                nums[pivot_idx], nums[j] = nums[j], nums[pivot_idx]
                j -= 1
        # After loop, pivot_idx will be the final position of the pivot
        # All elements before pivot_idx are less than pivot, all elements after pivot_idx are greater than or equal to pivot
        nums[right], nums[pivot_idx] = nums[pivot_idx], nums[right]
        return pivot_idx
        
    #You can also use iterative method instead of recursion method here
    #N.B. The k goes from 0, to n-1 here, k+1 is the normal meaning of k-th smallest in an array

    def find_kth_element(nums, left, right, k):
        if left == right:
            return nums[left]
        
        random_idx = random.randint(left, right)
        pivot = nums[random_idx]
        sorted_idx = find_pivot_index(nums, left, right, random_idx)
        if sorted_idx == k:
            return pivot
        elif sorted_idx < k:
            return find_kth_element(nums, sorted_idx+1, right, k)
        return find_kth_element(nums, left, sorted_idx-1, k)        


        #Iterative version
        uniques = list(counts.keys())
        N = len(uniques)
        left, right = 0, len(uniques)-1
        while left <= right:
            random_idx = random.randint(left, right)
            sorted_idx = find_pivot_index(uniques, left, right, random_idx)
            if sorted_idx == k:
                break
            elif sorted_idx > k:
                right = sorted_idx - 1
            else:
                left = sorted_idx + 1
        
        return  uniques[N-k:]

    ```    



[Quickselect]: https://leetcode.com/problems/kth-largest-element-in-an-array/solution/
