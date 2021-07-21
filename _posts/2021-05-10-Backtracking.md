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





[LC729. My Calendar I]: https://leetcode.com/problems/my-calendar-i/
[LC425 Word Squares]: https://leetcode.com/problems/word-squares/
[LC17. Letter Combinations of a Phone Number]: https://leetcode.com/problems/letter-combinations-of-a-phone-number/