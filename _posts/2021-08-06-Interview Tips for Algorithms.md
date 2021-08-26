---
title: "Interview Tips for Algorithmic Problems"
date: 2021-08-06
categories:
  - blog
tags:
  - algorithm
  - summary
---

1. Interview Tip: In-place Algorithms
    * In-place algorithms overwrite the input to save space, but sometimes this can cause problems. Here are a couple of situations where an in-place algorithm might not be suitable.
    * The algorithm needs to run in a multi-threaded environment, without exclusive access to the array. Other threads might need to read the array too, and might not expect it to be modified.
    * Even if there is only a single thread, or the algorithm has exclusive access to the array while running, the array might need to be reused later or by another thread once the lock has been released.
    * If you are asked to use `O(1)`, try think about re-using the input array if there's one.

2. Interview Tip: Practice Overriding Your Brains "Assume" Mode!
    1. We humans have a habit of making a lot of assumptions - neurobiologists reassure us that this is quite normal! If we didn't make lots of assumptions, our brains would slow to a crawl like a poorly maintained computer, thanks to the overload of additional information they'd have to process.
    2. In an interview situation, where most of us are at least a little nervous, we are even less likely to question our assumptions. The moment most of us realize that we can solve the problem using the top-to-bottom approach, we will be frantically coding it up to show our interviewer that we can solve the problem.
    3. But this isn't ideal! In an interview, and when solving difficult problems in general, **you need to learn to identify the assumptions you're making, and question them in your mind**. 
        * In some problems, this can be things like assuming that input is sorted, 
        * that there will be no invalid cases, 
        * that they won't mind you overwriting the input, 
        * or even that the environment is single-threaded. 
        * In this case, the assumption is assuming that the only way of solving this problem is to work from top to bottom.
    4. **The only way to get good at challenging your assumptions is lots of practice**. Working in a group with other people preparing for code interviews can help too - learning how other people see problems will widen your own way of seeing problems.

3. Calculate the complexity    
    1. A rule: `O(log n!) = O(n log n)` according to Stirling's formula
    2. You can drop lower order term to find the lower bound, e.g.                 
        * `O(nlogn) = O(n)`
        * `O(log(n!)⋅logn) = O(log(n!))`: drops `logn` as `log(n!)` is a lot bigger
    3. Compute the complexity of recursive function
        * [One of the best ways I find for approximating the complexity of the recursive algorithm][Determining complexity for recursive functions (Big O notation)] is drawing the recursion tree. Once you have the recursive tree:
            * Complexity = (length of tree from root node to leaf node) * (number of leaf nodes) *(time of each node)
        * 

    
    4. Problems
        * [LC172. Factorial Trailing Zeroes][LC172. Factorial Trailing Zeroes]



[LC172. Factorial Trailing Zeroes]: https://leetcode.com/problems/factorial-trailing-zeroes/
[Determining complexity for recursive functions (Big O notation)]: https://stackoverflow.com/questions/13467674/determining-complexity-for-recursive-functions-big-o-notation#comment113157141_43991156