---
title: "Dynamic Programming"
date: 2021-04-27
categories:
  - blog
tags:
  - algorithm
  - summary
  - dynamic programming
---

1. [动态规划解题套路框架][动态规划解题套路框架]
    1. 首先，动态规划问题的一般形式就是求最值. Example: 最长递增子序列呀，最小编辑距离    
    2. 求解动态规划的核心问题是穷举。因为要求最值，肯定要把所有可行的答案穷举出来，然后在其中找最值
        * 计算机解决问题其实没有任何奇技淫巧，它唯一的解决办法就是穷举，穷举所有可能性。算法设计无非就是先思考“如何穷举”，然后再追求“如何聪明地穷举”

2. 动态规划三要素
    1. 这类问题存在「重叠子问题」
        * 如果暴力穷举的话效率会极其低下，所以需要「备忘录」或者`「DP table」`来优化穷举过程，避免不必要的计算。
        * 如何一眼看出重叠子问题?
            * 首先，最简单粗暴的方式就是画图，把递归树画出来，看看有没有重复的节点。
            * 但稍加思考就可以知道，其实根本没必要画图，可以通过递归框架直接判断是否存在重叠子问题: 
                * 具体操作就是直接删掉代码细节，抽象出该解法的递归框架
    2. 具备「最优子结构」, 才能通过子问题的最值得到原问题的最值. 要符合「最优子结构」，子问题间必须互相独立
        * 遇到最优子结构失效情况 (子问题间不互相独立)，怎么办？策略是：改造问题.
        * 最优子结构并不是动态规划独有的一种性质，能求最值的问题大部分都具有这个性质；但反过来，最优子结构性质作为动态规划问题的必要条件，一定是让你求最值的，以后碰到那种恶心人的最值题，思路往动态规划想就对了，这就是套路.
        * 找最优子结构的过程，其实就是证明状态转移方程正确性的过程，方程符合最优子结构就可以写暴力解了，写出暴力解就可以看出有没有重叠子问题了，有则优化，无则 OK。这也是套路，经常刷题的读者应该能体会
    3. 只有列出正确的「状态转移方程」(recurrence relation)，才能正确地穷举. 千万不要看不起暴力解，动态规划问题最困难的就是写出这个暴力解，即状态转移方程
        * 明确 base case        
        * 明确「状态」，也就是原问题和子问题中会变化的变量
        * 明确「选择」，也就是导致「状态」产生变化的行为
        * 定义 dp 数组/函数的含义
        * 根据「选择」，思考状态转移的逻辑, 找到动态规划的状态转移关系
            * 动态规划的通用技巧：数学归纳思想
            * 明确 dp 数组的定义。这一步对于任何动态规划问题都很重要，如果不得当或者不够清晰，会阻碍之后的步骤。
            * 根据 dp 数组的定义，运用数学归纳法的思想，假设 dp[0...i-1] 都已知，想办法求出 dp[i]，一旦这一步完成，整个题目基本就解决了。
            * 但如果无法完成这一步，很可能就是 dp 数组的定义不够恰当，需要重新定义 dp 数组的含义；或者可能是 dp 数组存储的信息还不够，不足以推出下一步的答案，需要把 dp 数组扩大成二维数组甚至三维数组。

3. 动态规划解题套路
    ```
    # 初始化 base case
    dp[0][0][...] = base
    # 进行状态转移
    for 状态1 in 状态1的所有取值：
        for 状态2 in 状态2的所有取值：
            for ...
                dp[状态1][状态2][...] = 求最值(选择1，选择2...)
    ```

4. dp 数组的大小设置
    * 理论上，你怎么定义都可以，只要根据定义处理好 base case 就可以。

5. dp 数组的遍历方向
    * 遍历的过程中，所需的状态必须是已经计算出来的。
    * 遍历结束后，存储结果的那个位置必须已经被计算出来。

6. 空间压缩技巧
    * 能够使用空间压缩技巧的动态规划都是二维 `dp` 问题，你看它的状态转移方程，如果计算状态 `dp[i][j]` 需要的都是 `dp[i][j]` 相邻的状态，那么就可以使用空间压缩技巧，将二维的 `dp` 数组转化成一维，将空间复杂度从 `O(N^2)` 降低到 `O(N)`.
    * 空间压缩的核心思路就是，将二维数组「投影」到一维数组

7. How to realize that a problem is NOT a dynamic programming problem? 
    1. [One way to realize that it isn't dynamic programming][LC1631. Path With Minimum Effort] is to notice that the hiker can go in all four directions. This means that a dp algorithm would need to look into subproblems that haven't been solved yet.

8. [动态规划和回溯算法][LC494. Target Sum]
    1. 回溯算法和递归算法有点类似，有的问题如果实在想不出状态转移方程，尝试用回溯算法暴力解决也是一个聪明的策略，总比写不出来解法强
    2. 这个问题可以转化为一个子集划分问题，而子集划分问题又是一个典型的背包问题

9. Subsequence Type Problems
    0. 我总结出来做算法题的技巧就是，把大的问题细化到一个点，先研究在这个小的点上如何解决问题，然后再通过递归/迭代的方式扩展到整个问题。
    1. [Longest Increasing Subsequence (LIS, 最长递增子序列)][LC300. Longest Increasing Subsequence]
        1. Build up the subsequence one by one: `O(n^2)`
        2. Build up the subsequence using binary search, `O(nlogn)`
    2. [LC354. Russian Doll Envelopes][LC354. Russian Doll Envelopes]
    3. [LC72. Edit Distance][LC72. Edit Distance]
        1. 一般来说，处理两个字符串的动态规划问题，都是建立 DP table。
        2. 这里只求出了最小的编辑距离，那具体的操作是什么？
            * 给 dp 数组增加额外的信息即可. val 属性就是之前的 dp 数组的数值，choice 属性代表操作。在做最优选择时，顺便把操作记录下来，然后就从结果反推具体操作。
            ```
            // int[][] dp;
            Node[][] dp;

            class Node {
                int val;
                int choice;
                // 0 代表啥都不做
                // 1 代表插入
                // 2 代表删除
                // 3 代表替换
            }
            ```
    4. [LC53. Maximum Subarray][LC53. Maximum Subarray]
        1. 这道题还不能用滑动窗口算法，因为数组中的数字可以是负数。
    5. [LC1143. Longest Common Subsequence][LC1143. Longest Common Subsequence]
        1. 

10. Knapsack Type Problems
    1. 子集背包问题: [LC416. Partition Equal Subset Sum][LC416. Partition Equal Subset Sum]
    2. 完全背包问题: [LC518. Coin Change 2][518. Coin Change 2]

10. Greedy Type Problems

11. Game Type Problems
    1. [LC174. Dungeon Game][LC174. Dungeon Game]
    2. [514. Freedom Trail][514. Freedom Trail]

12. [Best Time to Buy and Sell Stock][Most consistent ways of dealing with the series of stock problems]

13. [Ugly Number][LC264. Ugly Number II]
    1. Since any existed number will be multiplied by 2, 3 and 5 once and only once, otherwise duplicate, we can use a pointer to keep track of where the 2, 3 and 5 are going to multiply in the next step.
    2. Once, we find the next minimum, we can move on the corresponding pointer, otherwise it always stays at the already existed ugly number which would makes pointer useless

14. 动态规划之最小路径和
    1. 一般来说，让你在二维矩阵中求最优化问题（最大值或者最小值），肯定需要递归 + 备忘录，也就是动态规划技巧。
    2. [LC64. Minimum Path Sum][LC64. Minimum Path Sum]
    

6. [Split a sequence in an optimal way (LC1335)][Minimum Difficulty of a Job Schedule]


7. [5 Steps to Think Through DP Problems][DP IS EASY! 5 Steps to Think Through DP Questions]
    0. DP Framework
    ```
    def dp(state variables):
        # base case
        # decision1, decision2 
        # return max(decision1, decision2)
    ```
    1. Category
        * Most dynamic programming questions can be boiled down to a few categories. It's important to recognize the category because it allows us to FRAME a new question into something we already know. Frame means use the framework, not copy an approach from another problem into the current problem. You must understand that every DP problem is different.
        * Question: Identify [this problem][LC494. Target Sum] as one of the categories below before continuing.
            * 0/1 Knapsack
            * Unbounded Knapsack
            * Shortest Path (eg: Unique Paths I/II)
            * Fibonacci Sequence (eg: House Thief, Jump Game)
            * Longest Common Substring/Subsequeunce
        * Answer: 0/1 Knapsack
            * Why 0/1 Knapsack? Our 'Capacity' is the target we want to reach 'S'. Our 'Items' are the numbers in the input subset and the 'Weights' of the items are the values of the numbers itself. This question follows 0/1 and not unbounded knapsack because we can use each number ONCE.
        * What is the variation? The twist on this problem from standard knapsack is that we must add ALL items in the subset to our knapsack. We can reframe the question into adding the positive or negative value of the current number to our knapsack in order to reach the target capacity 'S'.
    2. States
        * What variables we need to keep track of in order to reach our optimal result? This Quora post explains state beautifully, so please refer to [What-does-a-state-represent-in-terms-of-Dynamic-Programming on Quora][What-does-a-state-represent-in-terms-of-Dynamic-Programming] if you are confused: 
        * Question: Determine State variables.
            * Hint: As a general rule, Knapsack problems will require 2 states at minimum.
            * Answer: Index and Current Sum
                * Why Index? Index represents the index of the input subset we are considering. This tells us what values we have considered, what values we haven't considered, and what value we are currently considering. As a general rule, index is a required state in nearly all dynamic programming problems, except for shortest paths which is row and column instead of a single index but we'll get into that in a seperate post.
                * Why Current Sum? The question asks us if we can sum every item (either the positive or negative value of that item) in the subset to reach the target value. Current Sum gives us the sum of all the values we have processed so far. Our answer revolves around Current Sum being equal to Target.

    3. Decisions
        * Dynamic Programming is all about making the optimal decision. In order to make the optimal decision, we will have to try all decisions first. The MIT lecture on DP (highly recommended) refers to this as the guessing step. My brain works better calling this a decision instead of a guess. Decisions will have to bring us closer to the base case and lead us towards the question we want to answer. Base case is covered in Step 4 but really work in tandem with the decision step.
        * Question: What decisions do we have to make at each recursive call?
            * Hint: As a general rule, Knapsack problems will require 2 decisions.
            * Answer: This problem requires we take ALL items in our input subset, so at every step we will be adding an item to our knapsack. Remember, we stated in Step 2 that "The question asks us if we can sum every item (either the positive or negative value of that item) in the subset to reach the target value." The decision is:
                * Should we add the current numbers positive value
                * Should we add the current numbers negative value
            * As a note, knapsack problems usually don't require us to take all items, thus a usual knapsack decision is to take the item or leave the item.

    4. Base Case
        * Base cases need to relate directly to the conditions required by the answer we are seeking. This is why it is important for our decisions to work towards our base cases, as it means our decisions are working towards our answer.
        * Let's revisit the conditions for our answers.
            * We use all numbers in our input subset.
            * The sum of all numbers is equal to our target 'S'.
            * Question: Identify the base cases.
                * Hint: There are 2 base cases.
                * Answer: We need 2 base cases. One for when the current state is valid and one for when the current state is invalid.
                    * Valid: Index is out of bounds AND current sum is equal to target 'S'
                    * Invalid: Index is out of bounds
                    * Why Index is out of bounds? A condition for our answer is that we use EVERY item in our input subset. When the index is out of bounds, we know we have considered every item in our input subset.
                    * Why current sum is equal to target? A condition for our answer is that the sum of using either the positive or negative values of items in our input subet equal to the target sum 'S'.
                    * If we have considered all the items in our input subset and our current sum is equal to our target, we have successfully met both conditions required by our answer.
                    * On the other hand, if we have considered all the items in our input subset and our current sum is NOT equal to our target, we have only met condition required by our answer. No bueno.

    5. Code it
        * If you've thought through all the steps and understand the problem, it's trivial to code the actual solution.

    6. Optimize
        * Once we introduce memoization, we will only solve each subproblem ONCE. We can remove recursion altogether and avoid the overhead and potential of a stack overflow by introducing tabulation. It's important to note that the top down recursive and bottom up tabulation methods perform the EXACT same amount of work. The only different is memory. If they peform the exact same amount of work, the conversion just requires us to specify the order in which problems should be solved.

8. Dynamic programming requires the subproblem solved in topological order. In many problems, it coincides the natural order. For those who doesn't, e.g. in a graph, one need perform topological sorting first. Therefore, for those problems with complex topology ([like this one][LC329. Longest Increasing Path in a Matrix]), search with memorization is usually an easier and better choice.






[LC1631. Path With Minimum Effort]: https://leetcode.com/problems/path-with-minimum-effort/solution/
[Minimum Difficulty of a Job Schedule]: https://leetcode.com/problems/minimum-difficulty-of-a-job-schedule/
[LC264. Ugly Number II]: https://leetcode.com/problems/ugly-number-ii/
[LC300. Longest Increasing Subsequence]: https://leetcode.com/problems/longest-increasing-subsequence/
[LC416. Partition Equal Subset Sum]: https://leetcode.com/problems/partition-equal-subset-sum/
[DP IS EASY! 5 Steps to Think Through DP Questions]: https://leetcode.com/problems/target-sum/discuss/455024/DP-IS-EASY!-5-Steps-to-Think-Through-DP-Questions.
[LC494. Target Sum]: https://leetcode.com/problems/target-sum/
[What-does-a-state-represent-in-terms-of-Dynamic-Programming]: www.quora.com/What-does-a-state-represent-in-terms-of-Dynamic-Programming
[LC329. Longest Increasing Path in a Matrix]: https://leetcode.com/problems/longest-increasing-path-in-a-matrix/
[动态规划解题套路框架]: https://labuladong.github.io/algo/3/23/68/
[LC354. Russian Doll Envelopes]: https://leetcode.com/problems/russian-doll-envelopes/
[LC72. Edit Distance]: https://leetcode.com/problems/edit-distance/
[LC53. Maximum Subarray]: https://leetcode.com/problems/maximum-subarray/
[LC1143. Longest Common Subsequence]: https://leetcode.com/problems/longest-common-subsequence/
[经典动态规划：0-1 背包问题]: https://labuladong.github.io/algo/3/25/82/
[LC518. Coin Change 2]: https://leetcode.com/problems/coin-change-2/
[一个方法团灭 LEETCODE 股票买卖问题]: https://labuladong.github.io/algo/1/12/
[Most consistent ways of dealing with the series of stock problems]: https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-transaction-fee/discuss/108870/Most-consistent-ways-of-dealing-with-the-series-of-stock-problems
[LC64. Minimum Path Sum]: https://leetcode.com/problems/minimum-path-sum/
[LC174. Dungeon Game]: https://leetcode.com/problems/dungeon-game/
[514. Freedom Trail]: https://leetcode.com/problems/freedom-trail/