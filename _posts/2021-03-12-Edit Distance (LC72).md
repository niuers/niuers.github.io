---
title: "Edit Distance (LC72)"
date: 2021-03-12
categories:
  - blog
tags:
  - algorithm
  - leetcode
  - dynamic programming
---

1. Experience:
    1. It's a hard question for me. It's easy to understand the impact of 'delete' and 'replace'. However, I don't quite get how does 'insert' impact the result.
    2. I first tried some examples to get more intuition of the problem. 
        1. I tried to list out all possible edit available for a string. For example, 'horse', I can delete first letter 'h', replace it with 'r', and do insertion somewhere, this is the part that is uncertain to me because theoretically, you can insert at any position.
        2. So what am I doing here? I was trying to find a way to convert the current problem of transformation 'horse' to 'ros' into smaller problems, e.g. 'orse' -> 'ros', 'rorse' -> 'ros' etc. This looks like a tree structure. If I can list all possibilities out, then I can recursively call a function to compute the distance I need. 
        3. However, it turned out to be very complicate here:
            * We can insert at any position, which one shall I do such that I don't miss a solution?
            * We can also delete any letter in the string. I have to try each possibility to avoid missing out an optimal solution.
    3. I then thought maybe I should consider some simple cases first. 
        1. I tried the case to convert empty string to string of length 1, 2.
        2. I tried to convert string of length 1,2 to empty string, or string of length 1, 2.
        3. They are pretty straightforward to get the solutions.
        4. However, I didn't know how to utilize these simple cases to more complicate problems. How do I move from current stage to the next stage? What's the state transformation function? 
        5. At this time, I thought I had better to write out the recursive solution first to get a better idea of how might dynamic programming can solve this. I didn't think too much of what should the function return, what should the elements in dynamic table represent. 
    4. So I wrote a recursive function to solve the problem. 
        1. At first I thought I only need to do insert when the length of `word1` is smaller than `word2`. This is wrong, as we can see from `mart` -> `karma`.
        2. I also thought that I only need to do replacement when the lengths of two strings are the same. This is wrong too.
        3. It turned out that I had to try insert, replacement, and delete (at every position) for `word` to cover all the cases.
        4. This solution quickly got TLE for a smaller string length of 22.
    5. I really had no clue what to do now.
        1. I thought about aligning the two strings at different positions, and count for the differences in each alignment. It doesn't seem to help me much. 
    6. I started to look into the solution. The solution mentioned that I can use `dp[i][j]` to represent the 'edit distance' between string `word1[:i]` and `word2[:j]`. It hints me a lot. So I started to work on the dynamic table and see how can I get the transition formula.
        1. For the example, `horse` -> `ros`. I can work out the dynamic table easily. But I didn't quite get how we do the transition from previous cells to current cell.
        2. So I tried to figure out the pattern when we add a letter at the end of the current string. 
        3. The definition of the table element gives me direction to check with.
        4. I started with single letter `h` to single letter `r`, then two letters `ro`, then `ros` etc. As I worked on the example, I started to get more sense how does current cell relate to the previous cells.
        5. It's easy for me to understand the 'replacement' and 'delete' part. 
        6. It took me a while to figure out the case for `dp[i-1][j]`. I wasn't so sure why it works at the last position. Anyway, it seems to be the case here. 
        7. Once I found the meaning of `dp[i-1][j], dp[i][j-1], dp[i-1][j-1]`, it's easy to figure out the transition formula to `dp[i][j]`. 
        8. It's also immediate that I found the usage of edit distances for empty strings, which fit into the table perfectly.
    7. Now I have an implementation, it's another problem to prove that this is optimal. 
        1. Here's [some proof][Proof of edit distance solution] from internet.


2. How did I or Other people get the solution? 


3. Different solutions


4. Mistakes

5. Problem Type
    1. Dynamic programming
    2. Approximate String Match
    
6. Similar Problems


7. Template

8. I understand the solution, but HOW do I think to GET there myself?
  1. Where could you improve?
      1. I tried to work on complicate cases first and tried to find out the pattern to convert into smaller cases.
          * If I spent too much time on this, or it doesn't seem to be promising, I should stop and think about other solutions.
      2. Maybe I should always think about the simplest cases first.
          * Once I figure the simple cases, think out how should I expand to more complicate cases by adding extra letter.
          * One important thing is to determine the meaning of cells in the dynamic table. It's usually a good first guess to use whatever the problem is asking (in this case, the edit distance between two strings).           
  2. What questions should I ask myself so that I push myself closer to the solution? 
      1. Can we split this problem into smaller problems in a distinct way?
          * I tried first to decompose the problem of `horse`->`ros` into smaller problems but failed to find out clear pattern.
      2. Can we try simple cases first?
      3. How can we apply the results of simple cases to cases of just a little bit more complicate? For example, adding just 1 extra letter. 
      4. For such a bit more complicate problem, how can we classify it into different cases?
      5. Does our classification cover all the possible cases?
  3. What conclusions did I reach that I dropped some idea for the other? 
      1. The idea looks complicate, messy, time consuming, or no clear structure.
  4. How can I reach this conclusion faster ?
      1. Start from simple cases first, think about how to expand into more complicate cases.



Resources:
* [72. Edit Distance][LeetCode Link]


[LeetCode Link]: https://leetcode.com/problems/edit-distance/
[Proof of edit distance solution]: https://stackoverflow.com/questions/35835942/proof-of-correct-of-the-dynamic-programming-approach-to-min-edit-distance