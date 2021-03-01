---
title: "Russian Doll Envelopes (LC354)"
date: 2021-03-01
categories:
  - blog
tags:
  - algorithm
  - leetcode
  - longest increasing subsequence problem (LIS)
---

1. Experience:
  1. I started with a brutal force solution, where I sort the envelopes according to their width, height first. Then starting from the first envelope, for each envelope, check the count of all envelopes that can be put into this one.
    * I have to loop through all the previous envelopes to get the maximum count for the current envelope. Since some earlier envelope can contain much more envelopes than other envelope, where both of them can be put into current envelope. This is `O(n^2)` time complexity, however, it got TLE.
    * I realized that I only need to find the first envelope that can be put into current envelope and has the maximum counts on itself.
    * I then created an array where I save the count of envelopes that an envelope can hold along with the envelope's index. This array is sorted by the counts. At each envelope, I search from backwards, the first envelope that can be put into the current one will have the maximum possible envelopes we can put into current one. And we can break the loop here. Then I add the current envelope's count and index into the array and sort again. 
    * The above is implemented using `bisect.insort`. Although it has a theoretical time complexit of `O(n)`, in practice, it's much faster. This solution passed the tests with 16% ranking although theoretically it still has `O(n^2)` time complexity.
  2. The solution mentioned [the 1D longest increasing subsequence][1D Longest Increasing Subsequence], I went back to the problem and re-did it using above method, the rank went up to 68%.
    * It's possible to use recursive method as well, I should try it next time.
    * It turns out that the solution used a smart dynamic programming method to solve the problem. I can't really figure out that by myself!
    * [Here's a good explanation of the solution][The smallest tail dynamic programming solution]
  3. Knowing that this is a 2D longest increasing subsequence problem doesn't help me much solving the problem. Since I don't know how to apply the 1D `O(nlog(n))` solution here as we have 2 dimensions here, `w` and `h`, how should I order them? if I encounter a new envelope, which has a larger width but smaller height than the previous one, what should I do? Should I put it at the end of the sequence or should I use it to replace some envelope in the array, or should I just skip it?
    * I could not think through this without looking into the solutions.
    * It turns out to use some tricks here:
      * First, we sort with the width. Since any longest solution must have been sorted by the width first. Assumeing we have envelopes sorted by width, and we apply the 1D longest increasing subsequece solution on the heights, the resulting longest subsequence shall automatically be the longest subsequence in 2D. Right? 
      * The above is only correct when all envelopes have distinct width, when there are envelopes having the same width, the solution won't work.
      * They use a trick here by sorting with the height in descreasing order, this way, the longest subsequece will never include envelopes with the same width but different heights.

2. How did I or Other people get the solution? 


3. Different solutions




4. Mistakes

5. Problem Type
    * longest increasing subsequence problem (LIS)
    * I should be familiar with [the 1D LIS problem first][1D Longest Increasing Subsequence]: 

6. Similar Problems
  1. 


7. Template



Resources:
* [354. Russian Doll Envelopes][LeetCode Link]
* [300. Longest Increasing Subsequence][1D Longest Increasing Subsequence] 


[LeetCode Link]: https://leetcode.com/problems/russian-doll-envelopes/
[1D Longest Increasing Subsequence]: https://leetcode.com/problems/longest-increasing-subsequence/
[The smallest tail dynamic programming solution]: https://leetcode.com/problems/longest-increasing-subsequence/discuss/74824/JavaPython-Binary-search-O(nlogn)-time-with-explanation