---
title: "Making A Large Island (LC827)"
date: 2021-04-13
categories:
  - blog
tags:
  - algorithm
  - leetcode
  - DFS
---

1. Experience:
    1. I first thought about the brutal force solution: find all zeroes, check area if we flip it into one, get the maximum area. This is `O(n^4)` complexity.
    2. Then I thought that the problem is about the largest island size, it sounds like an optimal problem. Maybe I should try dynamic programming? So I tried to find some pattern when we expand the size of the grid. This seems complicate, as we increase the grid size, it changes the island size that we have previously computed. 
        * We can't decompose the problem easily into sub-problems.
    3. Then I thought about find the islands first. Sort them by areas, and try to connect the largest two to get the maximum areas.
    4. This seems to be workable. I thought we can find all clusters, while we are doing this, we can find their areas, and a set of boundaries (which are zeroes surrounding the island). This can all be done in `O(n^2)`. Then if I can loop through the islands, find the intersection of them and use it to compute the sum of areas.
        * This has a problem though, it works well for two islands, since I can get the intersection of them, if there's any, to compute the sum of islands (if they can be connected together). 
        * But how do I compute for the case where there are three or four islands that can be connected by only one zero. This requires me to do intersection for all combinations of islands. Definitely not `O(n^2)`
    5. The day after, I came up an idea where instead of saving the map from island to boundaries. If I have a map from each zero to a list of islands, I can easily compute the connected areas for each zero. 
        * This can be easily achieved if I have a map from island to zeroes first. I just need to reprocess the data reversely.
    6. My solution got accepted with 71% rank. But the memory rank is poor just 5%.


2. How did I or Other people get the solution? 
    1. The solution is similar to what I have here. Although it takes the freedome to change the original data, 'grid'. It assigns each grid with ones to its island identifier. The program looks cleaner.

3. Different solutions


4. Mistakes

5. Problem Type
    
6. Similar Problems

7. Template

8. I understand the solution, but HOW do I think to GET there myself?
    1. Where could you improve?
        * I should've written the DFS cleaner. This might be a candidate for template.
    2. What questions should I ask myself so that I push myself closer to the solution? 
    3. What conclusions did I reach that I dropped some idea for the other?
        * For dynamic programming, I need find sub-optimal problems. But this doesn't work here.
    4. How can I reach this conclusion faster ?
    



Resources:
* [827. Making A Large Island][LeetCode Link]


[LeetCode Link]: https://leetcode.com/problems/making-a-large-island/