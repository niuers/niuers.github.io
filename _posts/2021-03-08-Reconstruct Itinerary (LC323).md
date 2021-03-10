---
title: "Reconstruct Itinerary (LC323)"
date: 2021-03-08
categories:
  - blog
tags:
  - algorithm
  - leetcode
  - graph
  - greedy
  - Eulerian Path
---

1. Experience:
    1. This is a hard problem for me. A second try on this problem and I still can't get it through. 
    2. I first tried to store the destinations for each port and sort them with a priority queue. Then I wrote a recursive function which starts with "JFK". It'll check each destination on the start port, and call the function itself to see if it can go to the end (i.e. the itinerary has the length tickets plus 1). 
        * I spent a lot of time try to make this pass through the test cases, somehow I always missed some cases in my code. So I was struggling with how to move from current port to the next port such that we can go through all and each ticket exactly once. 
        * I was a bit confused by the termination condition as at the beginning, I wasn't sure about the requirement of "go through all and each ticket exactly once".
        * This didn't work though since I missed the case where there can be multiple flights from the same origin to the same destinations. Whereas I used a set to store the visited flights, which definitely mis-calculates in such cases.
    3. I thought more about the problem, and found some patterns here:
        * All the ports in the middle of the path must have equal number of in flights and out flights.
        * There are two cases for start and end ports: 
            * The start and end ports both have equal number of in and out flights, since we fixed the start port to be "JFK", the end port has to be "JFK" as well. 
            * The end port can only have one more number of in flights than the number of out flights. The start port can only have one more number of out flights than the number of in flights. 
        * However, I didn't know how to utilize the above information.
    4. The above observations help me understand the linear time Eulerian path solution. Although I don't have the proof that it'll work!

2. How did I or Other people get the solution? 


3. Different solutions




4. Mistakes

5. Problem Type
    * Graph
    * Eulerian Path
    * DFS

6. Similar Problems
  1. 


7. Template



Resources:
* [323. Reconstruct Itinerary][LeetCode Link]


[LeetCode Link]: https://leetcode.com/problems/reconstruct-itinerary/