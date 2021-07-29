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
        * The 2nd method is to sort the array first, and skip repeat number while searching for valid combinations. To think through why this works, consider an example array `[1,2,2,2,5]`. If we fix the first number with `1` (so our current combination array is `[1]`) and we are trying to search the combinations generated by the rest of numbers, i.e. `[2,2,3,5]`. Let's lable the `2` by `2a,2b,2c`, so we have `[1,2a,2b,2c,5]`. For any given length of combination, e.g. `k`, we have:
            * If we choose `2a` as our next number, our combination array becomes `[1, 2a]`, the rest of `k-2` numbers will be chosen from `[2b, 2c, 5]`. Notice here we have two paths, i.e. (1) Choose `2b` as the next number, and choose the rest `k-3` from `[2c, 5]`; (2) Choose the rest `k-2` numbers from `[2c, 5]`. These two choices combined give us all the combinations starting with `[1, 2a]`.
            * If we choose `2b` as our next number, our combination array becomes `[1, 2b]`, the rest of `k-2` numbers will be chosen from `[2c, 5]`. Notice this set of combinations is the same as the path (2) above given that `2a=2b`. So the set of combinations with `2b` is a subset of combinations when working with `2a`. By skipping `2b` in the same loop as `2a`, we ignore the same set of combinations that have been considered when working with `2a`.
        * The 3rd method is to generate a count of various numbers, and use that to search for valid combinations (reducing the count of a number by 1 when it's picked).
            * The use of a counter effectively remove the location differences of the same number. 
            * This ends up with the same set of combinations in the 2nd method above.
    4. Problems
        * [LC40. Combination Sum II][LC40. Combination Sum II]
        * [LC39. Combination Sum][LC39. Combination Sum]

6. Permutations
7. Subsets


[LC729. My Calendar I]: https://leetcode.com/problems/my-calendar-i/
[LC425 Word Squares]: https://leetcode.com/problems/word-squares/
[LC17. Letter Combinations of a Phone Number]: https://leetcode.com/problems/letter-combinations-of-a-phone-number/
[LC39. Combination Sum]: https://leetcode.com/problems/combination-sum/
[LC40. Combination Sum II]: https://leetcode.com/problems/combination-sum-ii/