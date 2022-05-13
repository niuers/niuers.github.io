---
title: "Backtracking"
date: 2021-05-05
categories:
  - blog
tags:
  - algorithm
  - summary
---

2. [回溯算法框架][回溯算法解题套路框架]    
    1. 其实回溯算法其实就是我们常说的 `DFS` 算法，本质上就是一种暴力穷举算法。复杂度一般都很高。
    2. 回溯算法就是个 `N` 叉树的前后序遍历问题，没有例外。解决一个回溯问题，实际上就是一个决策树的遍历过程。
    3. 回溯树就是回溯算法的「决策树」, 因为你在每个节点上其实都在做决策。可以把「路径」和「选择」列表作为决策树上每个节点的属性. 站在回溯树的一个节点上，你只需要思考 `3` 个问题：
        1. 路径：也就是已经做出的选择。
        2. 选择列表：也就是你当前可以做的选择。
        3. 结束条件：也就是到达决策树底层，无法再做选择的条件。
    4. 回溯算法的框架
    ```
    result = []
    
    // 写 backtrack 函数 (其实就像一个指针) 时，在这棵树上游走, 需要维护走过的「路径」和当前可以做的「选择列表」，
    // 当触发「结束条件」时，将「路径」记入结果集。其核心就是 for 循环里面的递归，在递归调用之前「做选择」，在递归调用之后「撤销选择」，特别简单
    def backtrack(路径, 选择列表):
        if 满足结束条件:
            result.add(路径)
            return
        
        for 选择 in 选择列表:
            做选择 // 前序遍历需要的操作
            backtrack(路径, 选择列表)
            撤销选择 // 后序遍历需要的操作
    ```
    5. 某种程度上说，动态规划的暴力求解阶段就是回溯算法。只是有的问题具有重叠子问题性质，可以用 `dp table` 或者备忘录优化，将递归树大幅剪枝，这就变成了动态规划。

3. Backtracking Template
```
def backtrack(candidate):
    if find_solution(candidate):
        output(candidate)
        return
    
    # iterate all possible candidates.
    for next_candidate in list_of_candidates:
        if is_valid(next_candidate):
            # try this partial candidate solution
            place(next_candidate)
            # given the candidate, explore further.
            backtrack(next_candidate)
            # backtrack
            remove(next_candidate)
```    

Example [LC17. Letter Combinations of a Phone Number][LC17. Letter Combinations of a Phone Number]:
```
mapping = {'2':'abc', '3':'def', '4':'ghi', '5':'jkl', '6':'mno', '7':'pqrs', '8':'tuv', '9':'wxyz'}
def backtrack(curr_pos, path, results):
    if len(path) == len(digits):
        results.append(''.join(path)) #O(N) for each combination
        return
    
    dig = digits[curr_pos]
    for ch in mapping[dig]:
        path.append(ch)
        backtrack(curr_pos+1, path, results)
        path.pop()
    
path, results = [], []
backtrack(0, path, results)
```


1. When do we need to backtrack when do we not?
    1. This is related to whether we need reset the value of an element once we finished visiting it.
    2. If we just need go through the path once, e.g. check if the path goes to the destination, then we don't need reset the value. 
    3. Examples
        * combinations: [LC17. Letter Combinations of a Phone Number][LC17. Letter Combinations of a Phone Number]

2. How to compute the time complexity of backtracking algorithm?
    * We know that the trace of the backtrack would form a n-ary tree. Therefore, the upper bound of the operations would be the total number of nodes in a full-blossom n-ary tree.
        * For example, In problem [425. Word Squares][LC425 Word Squares], at any node of the trace, at maximum it could have 26 branches (i.e. 26 alphabet letters). Therefore, the maximum number of nodes in a 26-ary tree would be approximately `26^L`, where `L` is the height of the tree.
        * To calculate a loose upper bound for the time complexity, let us consider it as a combination problem where the goal is to construct a sequence of a specific order, i.e. `|V_1V_2...V_n|`. For each position `V_i`, we could have `d` choices, i.e. at each airport one could have at most `d` possible destinations. Since the length of the sequence is `|E|`, the total number of combination would be `|E|^d`.
    * Don't forget to count the cost of processing just one of the combinations. For example, if you need loop an array to generate result for one combination, you need multiply `N` to the number of combinations computed above.
    * As we know, the maximal number of nodes in N-ary tree of height `h` would be `N^(h+1)`
    * You can also think of the total number of combinations for your result if it's suitable, that should be the upper bound for your backtrack.
        * While you  are doing this, don't forget the branches that don't end with the final leaves. For example, if you need pick `k` from `n` numbers which should satifying certain conditions. We shouldn't forget to count the combinations of `0`, `1`, `2`, .., `k-1` from `n`, which are the inner nodes in the combination tree. So we usually need to use the **sum of all nodes** to count the complexity.
    * In the execution graph (where common nodes are merged into one), we might visit certain nodes multiple times, but we visit each edge once and only once. Therefore, the time complexity of the algorithm is proportional to the number of edges. Then we need multiply the operations we have to do at each edge of the graph.
    * An example of computing the time complexity in a recursive problem. [139. Word Break, Comment by HugoZh in Solution][Example Time Complexity]


4. Here are a few notes about the above pseudocode.
    1. Overall, the enumeration of candidates is done in two levels: 
        * 1). at the first level, the function is implemented as recursion. At each occurrence of recursion, the function is one step further to the final solution.  
        * 2). as the second level, within the recursion, we have an iteration that allows us to explore all the candidates that are of the same progress to the final solution.

    2. The backtracking should happen at the level of the iteration within the recursion. 
    3. Unlike brute-force search, in backtracking algorithms we are often able to determine if a partial solution candidate is worth exploring further (i.e. is_valid(next_candidate)), which allows us to prune the search zones. This is also known as the constraint, e.g. the attacking zone of queen in N-queen game. 
    4. There are two symmetric functions that allow us to mark the decision (place(candidate)) and revert the decision (remove(candidate)).  
    5. Note the above code tries to add a candidate first into the solution and then remove it to try another candidate. Sometimes all solutions are valid, you can just use recursion to find all combinations from sub-problems and combine with current candidate. (Example, [LC17. Letter Combinations of a Phone Number][LC17. Letter Combinations of a Phone Number])

4. [无论是排列、组合还是子集问题，简单说无非就是让你从序列 `nums` 中以给定规则取若干元素，主要有以下几种变体][回溯算法秒杀所有排列/组合/子集问题]：
    1. 形式一: 元素无重不可复选，即 `nums` 中的元素都是唯一的，每个元素最多只能被使用一次，这也是最基本的形式。
        * 以组合为例，如果输入 `nums = [2,3,6,7]`，和为 `7` 的组合应该只有 `[7]`。
        ```
        /* 组合/子集问题回溯算法框架 */
        void backtrack(int[] nums, int start) {
            // 回溯算法标准框架
            for (int i = start; i < nums.length; i++) {
                // 做选择
                track.addLast(nums[i]);
                // 注意参数
                backtrack(nums, i + 1);
                // 撤销选择
                track.removeLast();
            }
        }

        /* 排列问题回溯算法框架 */
        void backtrack(int[] nums) {
            for (int i = 0; i < nums.length; i++) {
                // 剪枝逻辑
                if (used[i]) {
                    continue;
                }
                // 做选择
                used[i] = true;
                track.addLast(nums[i]);

                backtrack(nums);
                // 撤销选择
                track.removeLast();
                used[i] = false;
            }
        }
        ```
    2. 形式二: 元素可重不可复选，即 `nums` 中的元素可以存在重复，每个元素最多只能被使用一次。其关键在于排序和剪枝
        * 以组合为例，如果输入 `nums = [2,5,2,1,2]`，和为 `7` 的组合应该有两种 `[2,2,2,1]` 和 `[5,2]`。
        ```
        Arrays.sort(nums);
        /* 组合/子集问题回溯算法框架 */
        void backtrack(int[] nums, int start) {
            // 回溯算法标准框架
            for (int i = start; i < nums.length; i++) {
                // 剪枝逻辑，跳过值相同的相邻树枝
                if (i > start && nums[i] == nums[i - 1]) {
                    continue;
                }
                // 做选择
                track.addLast(nums[i]);
                // 注意参数
                backtrack(nums, i + 1);
                // 撤销选择
                track.removeLast();
            }
        }


        Arrays.sort(nums);
        /* 排列问题回溯算法框架 */
        void backtrack(int[] nums) {
            for (int i = 0; i < nums.length; i++) {
                // 剪枝逻辑
                if (used[i]) {
                    continue;
                }
                // 剪枝逻辑，固定相同的元素在排列中的相对位置
                if (i > 0 && nums[i] == nums[i - 1] && !used[i - 1]) {
                    continue;
                }
                // 做选择
                used[i] = true;
                track.addLast(nums[i]);

                backtrack(nums);
                // 撤销选择
                track.removeLast();
                used[i] = false;
            }
        }

        ```
    3. 形式三: 元素无重可复选，即 `nums` 中的元素都是唯一的，每个元素可以被使用若干次。只要删掉去重逻辑即可
        * 以组合为例，如果输入 nums = `[2,3,6,7]`，和为 `7` 的组合应该有两种 `[2,2,3]` 和 `[7]`。
        ```
        /* 组合/子集问题回溯算法框架 */
        void backtrack(int[] nums, int start) {
            // 回溯算法标准框架
            for (int i = start; i < nums.length; i++) {
                // 做选择
                track.addLast(nums[i]);
                // 注意参数
                backtrack(nums, i);
                // 撤销选择
                track.removeLast();
            }
        }

        /* 排列问题回溯算法框架 */
        void backtrack(int[] nums) {
            for (int i = 0; i < nums.length; i++) {
                // 做选择
                track.addLast(nums[i]);
                backtrack(nums);
                // 撤销选择
                track.removeLast();
            }
        }

        ```
    4. 但排列、组合、子集问题都可以有这三种基本形式，所以共有 9 种变化。
    5. 除此之外，题目也可以再添加各种限制条件，比如让你求和为 `target` 且元素个数为 `k` 的组合，那这么一来又可以衍生出一堆变体。但无论形式怎么变化，其本质就是穷举所有解，而这些解呈现树形结构，所以合理使用回溯算法框架，稍改代码框架即可把这些问题一网打尽。
    6. 记住如下组合/子集问题和排列问题的回溯树，就可以解决所有排列组合子集相关的问题. 首先，组合问题和子集问题其实是等价的 (大小为 `k` 的组合就是大小为 `k` 的子集)；至于之前说的三种变化形式，无非是在这两棵树上剪掉或者增加一些树枝罢了。
        * 标准的子集/组合问题是如何保证不重复使用元素的？答案在于 `backtrack` 递归时输入的参数 `start`: 这个 `i` 从 `start` 开始，那么下一层回溯树就是从 `start + 1` 开始，从而保证 `nums[start]` 这个元素不会被重复使用
        * 标准的全排列算法利用 `used` 数组进行剪枝，避免重复使用同一个元素。


5. Combinations
    1. 元素无重不可复选
        * [77. Combinations][77. Combinations]
    2. 元素可重不可复选
        * [LC40. Combination Sum II][LC40. Combination Sum II]: 说这是一个组合问题，其实换个问法就变成子集问题了：请你计算 candidates 中所有和为 target 的子集
    3. 元素无重可复选
        * [LC39. Combination Sum][LC39. Combination Sum]
    4. A brutal force is to try all the combinations one by one and check if they sum up to the target value. This can be done by fixing first number, then try all combinations from 2nd number on, then fixing the 2nd number, and try all combinations from 3rd number on, etc. This will have to try all combinations of `O(2^N-1)` for `N` numbers, as that's the total number of combinations with `N` numbers. 
        * The trick is that we pick the candidates **in order**. We treat the candidate as a list with order, e.g. `[1, 2, 3, 4, 5, 6, 7, 8. 9]`. At any given step, once we pick a number, e.g. `6`, we will not consider any digits before the chosen number for the following steps, e.g. the candidates are reduced down to `[7, 8, 9]`.
        * With the above strategy, we could ensure that a number will never be picked twice for the same combination. Also, all the combinations that we come up with would be unique.
    3. If there are duplicate numbers in the array, we need remove any duplicate combinations
        * A brutal force solultion is to try all combinations, and sort each combination before we insert it into a set. The resulting set won't include any duplicate. This still has `O(2^N-1)` complexity, with extra cost of `O(klogk)` for each combination where `k` is the average length of the combination.
        * The 2nd method is to sort the array first, and skip repeat number while searching for valid combinations. To think through why this works, consider an example array `[1,2,2,2,5]`. If we fix the first number with `1` (so our current combination array is `[1]`) and we are trying to search the combinations generated by the rest of numbers, i.e. `[2,2,3,5]`. Let's label the `2` by `2a,2b,2c`, so we have `[1,2a,2b,2c,5]`. For any given length of combination, e.g. `k`, we have:
            * If we choose `2a` as our next number, our combination array becomes `[1, 2a]`, the rest of `k-2` numbers will be chosen from `[2b, 2c, 5]`. Notice here we have two paths, i.e. (1) Choose `2b` as the next number, and choose the rest `k-3` from `[2c, 5]`; (2) Choose the rest `k-2` numbers from `[2c, 5]`. These two choices combined give us all the combinations starting with `[1, 2a]`.
            * If we choose `2b` as our next number, our combination array becomes `[1, 2b]`, the rest of `k-2` numbers will be chosen from `[2c, 5]`. Notice this set of combinations is the same as the path (2) above given that `2a=2b`. So the set of combinations with `2b` is a subset of combinations when working with `2a`. By skipping `2b` in the same loop as `2a`, we ignore the same set of combinations that have been considered when working with `2a`.
        * The 3rd method is to generate a count of various numbers, and use that to search for valid combinations (reducing the count of a number by 1 when it's picked).
            * The use of a counter effectively remove the location differences of the same number. 
            * N.B. We need convert the counts from dictionary to a list of tuples. In each call of backtrack, we have to move from current  index, otherwise, we'll have duplicates.
                * For example, `[2,5,2,1,2]`, which counts to `{2:3, 5:1, 1:1}`. Once we have processed all `2`, we should skip it in future calls, otherwise, we'll have duplicate, e.g. when we process `1`, we'll get `[1,2,2]` which is the same as `[2,2,1]` when we processed `2` previously.
            * This ends up with the same set of combinations in the 2nd method above.
    4. Lexicographic (binary sorted) combinations
        * Think of mapping the set of numbers (`1,2,...,n`) to a binary number
        * Initiate nums as a list of integers from `1` to `k`. Add `n + 1` as a last element, it will serve as a sentinel. Set the pointer in the beginning of the list `j = 0`.
        * While `j < k` : Add the first `k` elements from nums into the output, i.e. all elements but the sentinel. Find the first number in nums such that `nums[j]+ 1 != nums[j + 1]` and increase it by one `nums[j]++` to move to the next combination.
    5. [Factor combinations][LC254. Factor Combinations]
    6. Problems
        * [LC131. Palindrome Partitioning][LC131. Palindrome Partitioning]
            * In backtrack, suppose the complexity of size `n` is `T(n)`, for this problem, we can tell that in the worst case, `T(n) = T(n-1)+T(n-2)+...+T(2)+T(1)`. Similarly we have `T(n-1) = T(n-2)+...+T(2)+T(1)`, subtract from the previous equation, we have `T(n)=2T(n-1)`, by induction, we have `T(n) = 2^n`.
        * [LC254. Factor Combinations][LC254. Factor Combinations]

7. Subsets
    1. 元素无重不可复选
        * 我们通过保证元素之间的相对顺序不变来防止出现重复的子集。
        * 如果把根节点作为第 0 层，将每个节点和根节点之间树枝上的元素作为该节点的值，那么第 n 层的所有节点就是大小为 n 的所有子集。
        * 注意，本文之后所说「节点的值」都是指节点和根节点之间树枝上的元素，且将根节点认为是第 0 层。
        * [LC78. Subsets][LC78. Subsets]
    2. 元素可重不可复选
        * 我们需要进行剪枝，如果一个节点有多条值相同的树枝相邻，则只遍历第一条，剩下的都剪掉，不要去遍历. 体现在代码上，需要先进行排序，让相同的元素靠在一起，如果发现 nums[i] == nums[i-1]，则跳过
        * [LC90. Subsets II][LC90. Subsets II]
    3. 元素无重可复选
    1. Backtrack
        * The order of the subsets in the result is the preorder traversal of the recursion tree. All that is left to do is to code the solution. Sort the array first to avoid duplicates.
        * You can also use a counter
        * N.B. To avoid duplicates, we need to avoid adding duplicate while keeping the size of current subset the same as before. So that's why we need to increase the subset size when encounter a duplicate.
    2. Bitmasking
    3. Cascading
        * Whenever the element under consideration has duplicates, we add one of the duplicate elements to all the existing subsets to create new subsets. For the rest of the duplicates, we only add them to the subsets created in the previous step. By convention, whenever a value is encountered for the first time, we add it to all the existing subsets. Then onwards we add its duplicates only to the subsets created in the previous step.
        * We treat a group of duplicate elements as an array. Suppose we have an array `[3, 3, 3]`. The ways to add the elements from this array to the existing subsets are as follows:
            * Not add any element having value 3 in any subset.
            * Add one 3 in all the subsets.       
            * Add two 3 in all the subsets.
            * Add three 3 in all the subsets.            


8. Permutations
    1. 元素无重不可复选        
        * 排列问题本身就是让你穷举元素的位置，`nums[i]` 之后也可以出现 `nums[i]` 左边的元素，所以之前的那一套玩不转了，需要额外使用 `used` 数组来标记哪些元素还可以被选择。
        * [LC46. Permutations][LC46. Permutations]
    2. 元素可重不可复选
        * 所以现在的关键在于，如何设计剪枝逻辑，把这种重复去除掉？答案是，保证相同元素在排列中的相对位置保持不变。
            * 比如说 `nums = [1,2,2']` 这个例子，我保持排列中 `2` 一直在 `2'` 前面。
            * 标准全排列算法之所以出现重复，是因为把相同元素形成的排列序列视为不同的序列，但实际上它们应该是相同的；而如果固定相同元素形成的序列顺序，当然就避免了重复。
        * 当出现重复元素时，比如输入 `nums = [1,2,2',2'']`，`2'` 只有在 `2` 已经被使用的情况下才会被选择，同理，`2''` 只有在 `2'` 已经被使用的情况下才会被选择，这就保证了相同元素在排列中的相对位置保证固定。
        * [47. Permutations II][47. Permutations II]
    3. 元素无重可复选
        * 比如输入 `nums = [1,2,3]`，那么这种条件下的全排列共有 `3^3 = 27` 种
    1. A brutal force is to use a visited set to record the numbers that have been used. The loop in backtrack() function goes through each number in the original array but skip the ones in the visited set. Adding each new number into the 'track' until a valid permutation forms. This has the complexity of `O(N^N)`, which is much larger than the full set of permutations `O(N!)`.
    2. An improved method is to use an index to indicate the current start position of the permutation, and for each number after this index, we swap them with the number at the start position, then we proceed from there. This has time complexity of `O(N*N!)`, where the first `N` comes from the cost of copying the array while appending it into the result.
    3. To avoid duplicates:
        * A key insight to avoid generating any redundant permutation is that at each step rather than viewing each number as a candidate, we consider each unique number as the true candidate. For instance, at the very beginning, given in the input of [1, 1, 2], we have only two true candidates instead of three.
        * Use a counter
        * Sort the array first and then avoid using duplicate number that has been used previously. This is somehow tricky though as we can't use the swap method as we did when there's no duplicate numbers. This is because if we just sort and skip the swap with duplicate numbers, we can still have duplicate permutations, e.g. If the original array is `[-1, -1, 0, 0, 1, 1, 2]`, if at certain point, we have the prefix track of `[2, 1, 1]` and the rest array to be processed as `[0, -1, 0, -1]`. You can see that the rest array is not sorted anymore, and we can't just use the check `arr[i] == arr[i-1]` to test whether a number has been inserted, for example, the first and last `-1` can't be differentiated by this way. 
            * To solve this issue, we have to use an acciliary visited array and not swap the numbers.
            * Or you may use a set in each backtrack() call to check if the number has been used or not if you want to keep using swap.

8. General strategies to Combination/Permutation/Subsets Problems
    1. [There are generally three strategies to do it][LC78. Subsets]:
        * Recursion
        * Backtracking
        * Lexicographic generation based on the mapping between binary bitmasks and the corresponding permutations / combinations / subsets.
            * This method has the best time complexity, and as a bonus, it generates lexicographically sorted output for the sorted inputs
            * The idea is that we map each subset to a bitmask of length `n`, where `1` on the `ith` position in bitmask means the presence of `nums[i]` in the subset, and `0` means its absence.
            * Hence to solve the subset problem, we just need to generate `n` bitmasks from `0..00` to `1..11`
            * The real problem here is how to deal with zero left padding, because one has to generate bitmasks of fixed length, i.e. `001` and not just `1`. For that one could use standard bit manipulation trick. N.B. `bin(1)` produces `0b1`, not `0b0000...01`.
            ```
            nth_bit = 1 << n
            for i in range(2**n):
                # generate bitmask, from 0..00 to 1..11
                bitmask = bin(i | nth_bit)[3:]
            ```
            * or keep it simple stupid and shift iteration limits
            ```
            for i in range(2**n, 2**(n + 1)):
                # generate bitmask, from 0..00 to 1..11
                bitmask = bin(i)[3:]            
            ```
            * However, in this approach, some of the generated subsets will be duplicates. So we need to use an additional set, `seen` of type `string`, to detect duplicate subsets. In order to make use of `seen`, we must first sort the given array. Otherwise, `seen` won't be able to distinguish between duplicate subsets.

    


[LC729. My Calendar I]: https://leetcode.com/problems/my-calendar-i/
[LC425 Word Squares]: https://leetcode.com/problems/word-squares/
[LC17. Letter Combinations of a Phone Number]: https://leetcode.com/problems/letter-combinations-of-a-phone-number/
[LC39. Combination Sum]: https://leetcode.com/problems/combination-sum/
[LC40. Combination Sum II]: https://leetcode.com/problems/combination-sum-ii/
[LC46. Permutations]: https://leetcode.com/problems/permutations/
[LC78. Subsets]: https://leetcode.com/problems/subsets/
[LC90. Subsets II]: https://leetcode.com/problems/subsets-ii/
[LC131. Palindrome Partitioning]: https://leetcode.com/problems/palindrome-partitioning/
[LC254. Factor Combinations]: https://leetcode.com/problems/factor-combinations/
[LC139. Word Break]: https://leetcode.com/problems/word-break/
[LC140. Word Break II]: https://leetcode.com/problems/word-break-ii/
[Example Time Complexity]: https://leetcode.com/problems/word-break/solution/160312
[回溯算法解题套路框架]: https://labuladong.github.io/algo/1/5/
[回溯算法秒杀所有排列/组合/子集问题]: https://labuladong.github.io/algo/1/8/
[77. Combinations]: https://leetcode.com/problems/combinations/
[47. Permutations II]: https://leetcode.com/problems/permutations-ii/
