---
title: "Longest Valid Parentheses"
date: 2021-02-09
categories:
  - blog
tags:
  - algorithm
  - leetcode
  - dynamic programming
---

1. Experience:
    1. Wrote a brutal force solution first
        * loop through each character, find the longest valid parentheses starting with it. This is `O(n)` time complexity.
        * I used a counter to check the balance of `(` and `)`, whenever the counter goes to `0`, I compare current length with maximum length.
        * I had an error though where I forgot to break the inside loop when the number of `)` gets larger than that of `(`.
    2. I then started to work on a dynamic programming solution. 
        * At first, I was sure how to write out the transition function.
        * Then I decided to let `dp[i]` be the longest length of valid parentheses ending at index `i`. 
        * I then worked on the cases where `s[i]==(` and `s[i]==)`, also the cases depending on what `s[i-1]` is.
        * However, I missed the case when `s[i]==s[i-1]==)`, and also the string before `i-dp[i-1]-1` is another valid parentheses, with the help of test case, I fixed the problem and the solution got accepted.
        * This is an `O(n)` time complexity and `O(n)` space complexity algorithm.

2. How did I get the solution? 
    1. At first I thought I couldn't come up with an `O(n)` solution, then I went to the "solution" page, saw one of them is using "dynamic programming", this gave me confidence that dynamic programming shall work. So I focused on finding the transition function between `i` and `i+1`.
    2. To simplify the situation, I fixed `i` first, assuming that I have found the longest lenth of valid parenthese ending at `i`, then I thought on the relationships between `dp[i+1]` and `dp[i]`. 
    3. I tried to write out the formula for different cases, once it's written out, it's easy to write out the program. 

3. Different solutions
    1. There are four solutions for this problem, one is to use stack and the other one is to scan the string from left and right. 
    2. They are more specific to current problem though. However the dynamic programming can be applied to other problems as well.

4. Mistakes
    1. Missed couple of cases where the string can still be a valid parenthese.

5. Problem Type
    1. Problem Type: Find the longest length that satisfying some conditions in a longer string/array

6. Similar Problems

7. Template



Resources:
* [Longest Valid Parentheses][LeetCode Link]


[LeetCode Link]: https://leetcode.com/problems/longest-valid-parentheses/