---
title: "Backtracking"
date: 2021-05-05
categories:
  - blog
tags:
  - algorithm
  - summary
---

1. When do we need to backtrack when do we not?
    1. This is related to whether we need reset the value of an element once we finished visiting it.
    2. If we just need go through the path once, e.g. check if the path goes to the destination, then we don't need reset the value. 
    3. Examples
        * combinations: [LC17. Letter Combinations of a Phone Number][LC17. Letter Combinations of a Phone Number]

2. How to compute the time complexity of backtracking algorithm?
    * We know that the trace of the backtrack would form a n-ary tree. Therefore, the upper bound of the operations would be the total number of nodes in a full-blossom n-ary tree.
        * For example, In problem [425. Word Squares][LC425 Word Squares], at any node of the trace, at maximum it could have 26 branches (i.e. 26 alphabet letters). Therefore, the maximum number of nodes in a 26-ary tree would be approximately `26^L`, where `L` is the height of the tree.
    * Don't forget to count the cost of processing just one of the combinations. For example, if you need loop an array to generate result for one combination, you need multiply `N` to the number of combinations computed above.
    * As we know, the maximal number of nodes in N-ary tree of height `h` would be `N^(h+1)`
    * You can also think of the total number of combinations for your result if it's suitable, that should be the upper bound for your backtrack.

3. Backtracking Template
```
def backtrack(candidate):
    if find_solution(candidate):
        output(candidate)
        return
    
    # iterate all possible candidates.
    for next_candidate in list_of_candidates:
        if is_valid(next_candidate):
            # try this partial candidate solution
            place(next_candidate)
            # given the candidate, explore further.
            backtrack(next_candidate)
            # backtrack
            remove(next_candidate)
```    

Example [LC17. Letter Combinations of a Phone Number][LC17. Letter Combinations of a Phone Number]:
```
mapping = {'2':'abc', '3':'def', '4':'ghi', '5':'jkl', '6':'mno', '7':'pqrs', '8':'tuv', '9':'wxyz'}
def backtrack(curr_pos, path, results):
    if len(path) == len(digits):
        results.append(''.join(path)) #O(N) for each combination
        return
    
    dig = digits[curr_pos]
    for ch in mapping[dig]:
        path.append(ch)
        backtrack(curr_pos+1, path, results)
        path.pop()
    
path, results = [], []
backtrack(0, path, results)
```

4. Here are a few notes about the above pseudocode.
    1. Overall, the enumeration of candidates is done in two levels: 
        * 1). at the first level, the function is implemented as recursion. At each occurrence of recursion, the function is one step further to the final solution.  
        * 2). as the second level, within the recursion, we have an iteration that allows us to explore all the candidates that are of the same progress to the final solution.

    2. The backtracking should happen at the level of the iteration within the recursion. 
    3. Unlike brute-force search, in backtracking algorithms we are often able to determine if a partial solution candidate is worth exploring further (i.e. is_valid(next_candidate)), which allows us to prune the search zones. This is also known as the constraint, e.g. the attacking zone of queen in N-queen game. 
    4. There are two symmetric functions that allow us to mark the decision (place(candidate)) and revert the decision (remove(candidate)).  
    5. Note the above code tries to add a candidate first into the solution and then remove it to try another candidate. Sometimes all solutions are valid, you can just use recursion to find all combinations from sub-problems and combine with current candidate. (Example, [LC17. Letter Combinations of a Phone Number][LC17. Letter Combinations of a Phone Number])


5. Combinations
    1. In such problems, we are given an array of numbers (either with duplicates or without duplicates) and a target value, we are asked to find all combinations that sum to the target value. An important requirement is not to have any duplicate combinations in the result.
    2. A brutal force is to try all the combinations one by one and check if they sum up to the target value. This can be done by fixing first number, then try all combinations from 2nd number on, then fixing the 2nd number, and try all combinations from 3rd number on, etc. This will have to try all combinations of `O(2^N-1)` for `N` numbers, as that's the total number of combinations with `N` numbers. 
    3. If there are repeat numbers in the array, we need remove any duplicate combinations
        * A brutal force solultion is to try all combinations, and sort each combination before we insert it into a set. The resulting set won't include any duplicate. This still has `O(2^N-1)` complexity, with extra cost of `O(klogk)` for each combination where `k` is the average length of the combination.
        * The 2nd method is to sort the array first, and skip repeat number while searching for valid combinations. To think through why this works, consider an example array `[1,2,2,2,5]`. If we fix the first number with `1` (so our current combination array is `[1]`) and we are trying to search the combinations generated by the rest of numbers, i.e. `[2,2,3,5]`. Let's label the `2` by `2a,2b,2c`, so we have `[1,2a,2b,2c,5]`. For any given length of combination, e.g. `k`, we have:
            * If we choose `2a` as our next number, our combination array becomes `[1, 2a]`, the rest of `k-2` numbers will be chosen from `[2b, 2c, 5]`. Notice here we have two paths, i.e. (1) Choose `2b` as the next number, and choose the rest `k-3` from `[2c, 5]`; (2) Choose the rest `k-2` numbers from `[2c, 5]`. These two choices combined give us all the combinations starting with `[1, 2a]`.
            * If we choose `2b` as our next number, our combination array becomes `[1, 2b]`, the rest of `k-2` numbers will be chosen from `[2c, 5]`. Notice this set of combinations is the same as the path (2) above given that `2a=2b`. So the set of combinations with `2b` is a subset of combinations when working with `2a`. By skipping `2b` in the same loop as `2a`, we ignore the same set of combinations that have been considered when working with `2a`.
        * The 3rd method is to generate a count of various numbers, and use that to search for valid combinations (reducing the count of a number by 1 when it's picked).
            * The use of a counter effectively remove the location differences of the same number. 
            * This ends up with the same set of combinations in the 2nd method above.
    4. Lexicographic (binary sorted) combinations
        * Think of mapping the set of numbers (`1,2,...,n`) to a binary number
        * Initiate nums as a list of integers from `1` to `k`. Add `n + 1` as a last element, it will serve as a sentinel. Set the pointer in the beginning of the list `j = 0`.
        * While `j < k` : Add the first `k` elements from nums into the output, i.e. all elements but the sentinel. Find the first number in nums such that `nums[j]+ 1 != nums[j + 1]` and increase it by one `nums[j]++` to move to the next combination.


    5. Problems
        * [LC40. Combination Sum II][LC40. Combination Sum II]
        * [LC39. Combination Sum][LC39. Combination Sum]
        * [LC131. Palindrome Partitioning][LC131. Palindrome Partitioning]
            * In backtrack, suppose the complexity of size `n` is `T(n)`, for this problem, we can tell that in the worst case, `T(n) = T(n-1)+T(n-2)+...+T(2)+T(1)`. Similarly we have `T(n-1) = T(n-2)+...+T(2)+T(1)`, subtract from the previous equation, we have `T(n)=2T(n-1)`, by induction, we have `T(n) = 2^n`.

6. Permutations
    1. A brutal force is to use a visited set to record the numbers that have been used. The loop in backtrack() function goes through each number in the original array but skip the ones in the visited set. Adding each new number into the 'track' until a valid permutation forms. This has the complexity of `O(N^N)`, which is much larger than the full set of permutations `O(N!)`.
    2. An improved method is to use an index to indicate the current start position of the permutation, and for each number after this index, we swap them with the number at the start position, then we proceed from there. This has time complexity of `O(N*N!)`, where the first `N` comes from the cost of copying the array while appending it into the result.
    3. To avoid duplicates:
        * A key insight to avoid generating any redundant permutation is that at each step rather than viewing each number as a candidate, we consider each unique number as the true candidate. For instance, at the very beginning, given in the input of [1, 1, 2], we have only two true candidates instead of three.
        * Use a counter
        * Sort the array first and then avoid using duplicate number that has been used previously. This is somehow tricky though as we can't use the swap method as we did when there's no duplicate numbers. This is because if we just sort and skip the swap with duplicate numbers, we can still have duplicate permutations, e.g. If the original array is `[-1, -1, 0, 0, 1, 1, 2]`, if at certain point, we have the prefix track of `[2, 1, 1]` and the rest array to be processed as `[0, -1, 0, -1]`. You can see that the rest array is not sorted anymore, and we can't just use the check `arr[i] == arr[i-1]` to test whether a number has been inserted, for example, the first and last `-1` can't be differentiated by this way. 
            * To solve this issue, we have to use an acciliary visited array and not swap the numbers.
            * Or you may use a set in each backtrack() call to check if the number has been used or not if you want to keep using swap.

    4. Problems
        * [LC46. Permutations][LC46. Permutations]

7. Subsets
    1. Backtrack
        * The order of the subsets in the result is the preorder traversal of the recursion tree. All that is left to do is to code the solution. Sort the array first to avoid duplicates.
        * You can also use a counter
        * N.B. To avoid duplicates, we need to avoid adding duplicate while keeping the size of current subset the same as before. So that's why we need to increase the subset size when encounter a duplicate.
    2. Bitmasking
    3. Cascading
        * Whenever the element under consideration has duplicates, we add one of the duplicate elements to all the existing subsets to create new subsets. For the rest of the duplicates, we only add them to the subsets created in the previous step. By convention, whenever a value is encountered for the first time, we add it to all the existing subsets. Then onwards we add its duplicates only to the subsets created in the previous step.
        * We treat a group of duplicate elements as an array. Suppose we have an array `[3, 3, 3]`. The ways to add the elements from this array to the existing subsets are as follows:
            * Not add any element having value 3 in any subset.
            * Add one 3 in all the subsets.       
            * Add two 3 in all the subsets.
            * Add three 3 in all the subsets.            
    4. Problems
        * [LC78. Subsets][LC78. Subsets]
        * [LC90. Subsets II][LC90. Subsets II]


8. General strategies to Combination/Permutation/Subsets Problems
    1. [There are generally three strategies to do it][LC78. Subsets]:
        * Recursion
        * Backtracking
        * Lexicographic generation based on the mapping between binary bitmasks and the corresponding permutations / combinations / subsets.
            * This method has the best time complexity, and as a bonus, it generates lexicographically sorted output for the sorted inputs
            * The idea is that we map each subset to a bitmask of length `n`, where `1` on the `ith` position in bitmask means the presence of `nums[i]` in the subset, and `0` means its absence.
            * Hence to solve the subset problem, we just need to generate `n` bitmasks from `0..00` to `1..11`
            * The real problem here is how to deal with zero left padding, because one has to generate bitmasks of fixed length, i.e. `001` and not just `1`. For that one could use standard bit manipulation trick. N.B. `bin(1)` produces `0b1`, not `0b0000...01`.
            ```
            nth_bit = 1 << n
            for i in range(2**n):
                # generate bitmask, from 0..00 to 1..11
                bitmask = bin(i | nth_bit)[3:]
            ```
            * or keep it simple stupid and shift iteration limits
            ```
            for i in range(2**n, 2**(n + 1)):
                # generate bitmask, from 0..00 to 1..11
                bitmask = bin(i)[3:]            
            ```
            * However, in this approach, some of the generated subsets will be duplicates. So we need to use an additional set, `seen` of type `string`, to detect duplicate subsets. In order to make use of `seen`, we must first sort the given array. Otherwise, seen won't be able to distinguish between duplicate subsets.

    


[LC729. My Calendar I]: https://leetcode.com/problems/my-calendar-i/
[LC425 Word Squares]: https://leetcode.com/problems/word-squares/
[LC17. Letter Combinations of a Phone Number]: https://leetcode.com/problems/letter-combinations-of-a-phone-number/
[LC39. Combination Sum]: https://leetcode.com/problems/combination-sum/
[LC40. Combination Sum II]: https://leetcode.com/problems/combination-sum-ii/
[LC46. Permutations]: https://leetcode.com/problems/permutations/
[LC78. Subsets]: https://leetcode.com/problems/subsets/
[LC90. Subsets II]: https://leetcode.com/problems/subsets-ii/
[LC131. Palindrome Partitioning]: https://leetcode.com/problems/palindrome-partitioning/