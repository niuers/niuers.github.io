---
title: "My Calendar III (LC732)"
date: 2021-06-10
categories:
  - blog
tags:
  - algorithm
  - leetcode
---

1. Experience:
    1. I couldn't find a clean way to count the overlaps among different bookings, so I took a look at the solution.
    2. 


2. How did I or Other people get the solution? 

3. Different solutions

4. Mistakes


5. Problem Type
    1. This is to find the maximum number of concurrent ongoing event at any time.
        * We can log the `start` & `end` of each event on the timeline, each `start` add a new ongoing event at that time, each `end` terminate an ongoing event. Then we can scan the timeline to figure out the maximum number of ongoing event at any time.
        * When we encounter an ending event, that means that some meeting that started earlier has ended now. We are not really concerned with which meeting has ended. All we need is that some event ended.
        * The most intuitive data structure for timeline would be `array`, but the time spot we have could be very sparse, so we can use `sorted map` (TreeMap in Java, TreeMap is a map implementation that keeps its entries sorted according to the natural ordering of its keys) to simulate the time line to save space.



    
6. Similar Problems
    1. All the "My Calendar" problems can be solved by the solution of "Meeting Room 2" (LC253)
        * LC253 can also be solved with a priority queue using the ending time as key. 

7. Template

8. I understand the solution, but HOW do I think to GET there myself?
    1. Where could you improve?
    2. What questions should I ask myself so that I push myself closer to the solution? 
    3. What conclusions did I reach that I dropped some idea for the other?
    4. How can I reach this conclusion faster ?
    



Resources:
* [732. My Calendar III][LeetCode Link]


[LeetCode Link]: https://leetcode.com/problems/my-calendar-iii/