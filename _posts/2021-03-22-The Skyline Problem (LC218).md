---
title: "The Skyline Problem (LC218)"
date: 2021-03-22
categories:
  - blog
tags:
  - algorithm
  - leetcode
  - Priority Queue
---

1. Experience:
    1. I first asked the question: Can I build the skyline by adding the building one by one? 
        * It's not straightforward to me. I was thinking that for each building, I have to find out the intersections of all other buildings to it to be able to find out the skyline.
        * The algorithm looks like `O(n^2)`
    2. I then asked: How to find the structure of the problem? 
        * I don't have much clue. Felt like no starting point to crack the problem.
        * I tried several simple cases, it seems pretty complicate to me.
        * I couldn't find a pattern of the problem. I mean a one sentence conclusion that can give us the definitely answer for the skyline.
    3. I then asked: This is a 2D problem, How do I reduce it to 1D?
    4. I then started a new page, tried to summarize all the different cases when two buildings intersect with each other. 
        * However, I still couldn't summarize out the pattern here which may help me write the code.
    5. I thought about another method again.
        * I go through each x-coordinate, either beginning or ending point of the buildings.
        * For each x-coordinate, I found out the list of buildings that cover this x-coordinate. It's basically a list of heights relevant at this location.
        * I realized that at any given location, only the top 2 highest heights are relevant. Depending on whether it's the beginning/middle part of previous building and beginning of current or it's the end of previous and middle/end of current building, we can choose the skyline knots properly.
        * This sounds more clear for me, but I thought it's also `O(n^2)`, so I kept searching for new methods.
    6. I didn't write any solution on my own.


2. How did I or Other people get the solution? 
    1. I checked the solution provided by LeetCode. They use the divide and conquer method. 
        * I was wondering how did they get to the method?
        * I am a bit in doubt about their merge. I thought they should explain how to merge two skylines instead of just two buildings which is much simpler to explain and understand.
    2. There are better solution provided by other people.
        * They separate each building into left and right with height first and sort them in certain order.
        * They use a priority queue to store them.
        * Whenever we see a starting line, we add it into the queue
        * Whenever we see an ending line, we remove it from the queue.
        * After above steps, if the current maximum height has changed, we append the current x-coordinate and previous maximum height into the result.
        * I wrote the solution based on such method. There are several technique issues to solve first
            * Python doesn't have built-in `O(log(n))` removal method for priority queue. 
            * We need sort the lines in certain order and deal with some corner cases. This requires customized sorting.



3. Different solutions


4. Mistakes

5. Problem Type
    
6. Similar Problems

7. Template

8. I understand the solution, but HOW do I think to GET there myself?
    1. Where could you improve?
        1. Maybe I should write out the `O(n^2)` solution even if I think it's probably got TLE and complicate.
    2. What questions should I ask myself so that I push myself closer to the solution? 
        1. Maybe I should have a list of methods that I can ask myself:
            * Have you tried divide and conquer, dynamic programming, recursive, greedy etc.
    3. What conclusions did I reach that I dropped some idea for the other?
        1. When I couldn't clearly speak out the rule to determine the skyline.
        2. Next time, maybe I should ask:
            1. Given that there are several buildings overlapped, how do we determine the skyline? Can you do it in 1-2 sentences with clear definition.
    4. How can I reach this conclusion faster ?
    



Resources:
* [218. The Skyline Problem][LeetCode Link]


[LeetCode Link]: https://leetcode.com/problems/the-skyline-problem/