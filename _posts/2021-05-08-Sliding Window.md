---
title: "Sliding Window"
date: 2022-04-2 0
categories:
  - blog
tags:
  - algorithm
  - sliding window
  - summary
---

1. [滑动窗口算法][滑动窗口算法]:
  1. 滑动窗口算法就是专门处理子串/子数组问题的
  2. 滑动窗口算法框架: 其中两处 `...` 表示的更新窗口数据的地方，到时候你直接往里面填就行了。
  ```
  /* 滑动窗口算法框架 */
  void slidingWindow(string s, string t) {
      unordered_map<char, int> need, window;
      for (char c : t) need[c]++;
      
      int left = 0, right = 0;
      int valid = 0; 
      while (right < s.size()) {
          // c 是将移入窗口的字符
          char c = s[right];
          // 增大窗口
          right++;
          // 进行窗口内数据的一系列更新
          ...

          /*** debug 输出的位置 ***/
          printf("window: [%d, %d)\n", left, right);
          /********************/
          
          // 判断左侧窗口是否要收缩
          while (window needs shrink) {
              // d 是将移出窗口的字符
              char d = s[left];
              // 缩小窗口
              left++;
              // 进行窗口内数据的一系列更新
              ...
          }
      }
  }
  ```
  3. 初始化 `left = right = 0`，把索引左闭右开区间 `[left, right)` 称为一个「窗口」。理论上你可以设计两端都开或者两端都闭的区间，但设计为左闭右开区间是最方便处理的。因为这样初始化 `left = right = 0` 时区间 `[0, 0)` 中没有元素，但只要让 `right` 向右移动（扩大）一位，区间 `[0, 1)` 就包含一个元素 `0` 了。如果你设置为两端都开的区间，那么让 `right` 向右移动一位后开区间 `(0, 1)` 仍然没有元素；如果你设置为两端都闭的区间，那么初始区间 `[0, 0]` 就包含了一个元素。这两种情况都会给边界处理带来不必要的麻烦。
  4. 现在开始套模板，只需要思考以下四个问题：
    * 当移动 `right` 扩大窗口，即加入字符时，应该更新哪些数据？
    * 什么条件下，窗口应该暂停扩大，开始移动 `left` 缩小窗口？
    * 当移动 `left` 缩小窗口，即移出字符时，应该更新哪些数据？
    * 我们要的结果应该在扩大窗口时还是缩小窗口时进行更新？
  5. [LC76. Minimum Window Substring][LC76. Minimum Window Substring]

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
[滑动窗口算法]: https://labuladong.github.io/algo/1/11/