---
title: "Sliding Window"
date: 2021-05-10
categories:
  - blog
tags:
  - algorithm
  - sliding window
  - summary
---

1. With the two pointers, we can consider save following information along with:
  1. The right most position
  2. The count of characters
  3. Problems
      * [LC159. Longest Substring with At Most Two Distinct Characters][LC159. Longest Substring with At Most Two Distinct Characters]
      * [LC3. Longest Substring Without Repeating Characters][LC3. Longest Substring Without Repeating Characters]

2. [General summary of what kind of problem can/cannot solved by Two Pointers][General summary of what kind of problem can/ cannot solved by Two Pointers]
  1. A problem can be solved by two pointers when two pointers come into place to help us reduce the total cases we need to consider, such that the corresponding time complexity will reduce too.
  2. We can't solve a problem by two pointers if:
    * When a narrower scope of the sliding window (with maximum possible size) is valid, but a wider scope of that narrower scope can still be valid with the sizes between as invalid.

3. [Sliding Window Template][Here is a 10-line template that can solve most 'substring' problems]
  1. Template: For most substring problem, we are given a string and need to find a substring of it which satisfy some restrictions. A general way is to use a hashmap assisted with two pointers. The template is given below.

  ```
  int findSubstring(string s){
          vector<int> map(128,0);
          int counter; // check whether the substring is valid
          int begin=0, end=0; //two pointers, one point to tail and one  head
          int d; //the length of substring

          for() { /* initialize the hash map here */ }

          while(end<s.size()){

              if(map[s[end++]]-- ?){  /* modify counter here */ }

              while(/* counter condition */){ 
                  
                  /* update d here if finding minimum*/

                  //increase begin to make it invalid/valid again
                  
                  if(map[s[begin++]]++ ?){ /*modify counter here*/ }
              }  

              /* update d here if finding maximum*/
          }
          return d;
    }

  ```

  ```
  # start & end of sliding window: |start-> ... end->|
  # short version of sliding window, focus on two pointers
  def start_end_sliding_window(self, seq):
      start, end = 0, 0
      while end < len(seq):
          # end pointer grows in the outer loop
          end += 1
          
          # start pointer grows with some restrict
          while self.start_condition(start):
              # process logic before pointers movement
              self.process_logic1(start, end)
              # start grows in the inner loop
              start += 1
              
          # or process logic after pointers movement
          self.process_logic2(start, end)

  ```
  2. One thing needs to be mentioned is that when asked to find maximum substring, we should update maximum after the inner while loop to guarantee that the substring is valid. On the other hand, when asked to find minimum substring, we should update minimum inside the inner while loop.



[LC159. Longest Substring with At Most Two Distinct Characters]: https://leetcode.com/problems/longest-substring-with-at-most-two-distinct-characters/
[General summary of what kind of problem can/ cannot solved by Two Pointers]: https://leetcode.com/problems/subarray-sum-equals-k/discuss/301242/General-summary-of-what-kind-of-problem-can-cannot-solved-by-Two-Pointers
[LC3. Longest Substring Without Repeating Characters]: https://leetcode.com/problems/longest-substring-without-repeating-characters/
[LC560. Subarray Sum Equals K]: https://leetcode.com/problems/subarray-sum-equals-k/
[LC76. Minimum Window Substring]: https://leetcode.com/problems/minimum-window-substring/
[Here is a 10-line template that can solve most 'substring' problems]: https://leetcode.com/problems/minimum-window-substring/discuss/26808/Here-is-a-10-line-template-that-can-solve-most-'substring'-problems
