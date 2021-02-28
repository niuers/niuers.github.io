---
title: "Rearrange String k Distance Apart (LC358)"
date: 2021-02-28
categories:
  - blog
tags:
  - algorithm
  - leetcode
  - Greedy
---

1. Experience:
  1. At the beginning, I was trying to arrange the most frequent character in the array first, then tried to arrage other characters. 
    * It's hard to figure out the pattern from previous arrangement to the current arrangement.
    * Even for the most frequent character, there's more than 1 way to arrange it. As we can move the 2nd placement at the right of the 1st placement in positions of `k,k+1,...`. 
  2. So it seemed not work following this line of thought, then I started to think about how to iterate over all possibilities of arrangement and pick the one satisfying the condition. It sounds prohibitively complicate.
  3. I then thought about if there's a substring that satisfying the condition, what happens if I add a new character.
    * We can only choose from characters that haven't appeared in the last `k-1` positions.
    * We better select characters with the highest frequency (of updated counts), otherwise we may risk of not having enough spaces in the end of the string
    * This looks reasonablely clear and correct. So I started to implement this algorithm.
  4. I wanted to be able to find the maximum frequency fast, so I started with a dictionary which has each unique character as key and counts as value, a second dictionary with the count as key and list of characters as value, then I create a sorted list of the counts, so I can easily find the maximum value.
    * The implementation looks not that clean, but it got accepted.
    * I then started to improve the solution.
    * I noticed that I don't need the second dictionary and the sorted list, on each position, I can just search the first dictionary, and find the maximum frequency and corresponding character.
    * This cleans up the algorithm a lot, as I don't have to maintain too many data structures. This has a time complexity of `O(n^2)`
  5. By looking into the titles of the solutions, I know that there're `O(nlogn)` and `O(n)` algorithms. 
    * As I know already that a priority queue shall help to improve the algorithm to `O(nlogn)`, as I only need `log(n)` time to search for the most frequent character in a priority queue.
    * I started to implement this using python's heap. It makes the solution a bit more complex, but improved to 20% ranking. Still not that great, but much better than the 5% with `O(n^2)` complexity.
    * I then read the solutions from other people, looks like they are also using priority queue, but smarter than me on some details, for example, on each position, I did loop through the last `k-1` characters in the current string to skip through the characters that I shouldn't place. This might make the algorithm slower, since `k` can be as large as 26. (I realized this after reading the solution). If `k>26`, we won't be able to find a solution for any string.
    * Other people used another deque to store the used characters, instead of checking whether each character is in the deque each time, they first fill the deque up to `k`, then just pop left one character each time, it's guaranteed that the new character won't in the deque, and after we finish processing it, the popped character is put back into the heap if necessary.
    * As they can write customized comparison function for a heap with `(key, value) = (char, count)`, as compared to my `(count, char)` heap, their heap size won't exceed 26. So the actually time complexity is `O(nlog26)`, which is just `O(n)`.

2. How did I or Other people get the solution? 


3. Different solutions




4. Mistakes

5. Problem Type
    * Greedy Method

6. Similar Problems
  1. 


7. Template



Resources:
* [358. Rearrange String k Distance Apart][LeetCode Link]


[LeetCode Link]: https://leetcode.com/problems/rearrange-string-k-distance-apart/