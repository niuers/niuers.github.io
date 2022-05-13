---
title: "Randomized Algorithms"
date: 2021-09-13
categories:
  - blog
tags:
  - algorithm
  - summary
---

1. Randomized Sampling
  1. [Reservoir sampling][LC382. Linked List Random Node] to sample `k` elements from a population of unknown size (Algorithm R by Alan Waterman)
    ```
    # S has items to sample, R will contain the result
    def ReservoirSample(S[1..n], R[1..k])
      # fill the reservoir array
      for i := 1 to k
          R[i] := S[i]

      # replace elements with gradually decreasing probability
      for i := k+1 to n
        # randomInteger(a, b) generates a uniform integer
        #   from the inclusive range [a, ..., b])
        j := randomInteger(1, i)
        if j <= k
            R[j] := S[i]
    ```
    * Step 1: Store the first `k` elements.
    * Step 2: Every time we see the `i-th` element we select to use it with `k/i` probability. If so then we have randomly knocked off any one of (the `j-th` element) the already existing `k` elements in the storage uniformly (with probability `1/k`) and replace it with the selected element.
    * We can use induction to prove this
      * Given the current `i` numbers seen so far, assume that the probability of each number being in the buffer is `k/i`
      * Now we see the `(i+1)th` number, 
        * Item `(i+1)` is seen and is accepted with probability `k/(i+1)`.
        * The probability of any given item `j < i + 1` is in the buffer can be written down as: `P(item j was in the buffer)× P(item j is not removed) = P(item j was in the buffer)×[1 − P(item i+1 was accepted)P(item i was removed from the buffer) = k/i[1- k/(i+1)*1/k] = k/(i+1)`
    * Initially, we fill up an array of reservoir R[] with the heading elements from the pool of samples S[]. At the end of the algorithm, the reservoir will contain the final elements we sample from the pool.
    * We then iterate through the rest of elements in the pool. For each element, we need to decide if we want to include it in the reservoir or not. If so, we will replace an existing element in reservoir with the current element.
    * Given the above algorithm, it is guaranteed that at any moment, for each element scanned so far, it has an equal chance to be selected into the reservoir.
    * To sum up, in order for any element in the pool to be chosen in the final reservoir, a series of independent events need to occur, namely:
      * Firstly, the element needs to be chosen in the reservoir when we reach the element.
      * Secondly, in the following sampling, the element should remain in the reservoir, i.e. not to be replaced.

  1. [Resources][Reservoir Sampling]


2. Python `random`
    1. `random.choice(seq)`: Return a random element from the non-empty sequence `seq`. If `seq` is empty, raises `IndexError`. 
      * Time complexity? 
    2. `random.randint(a,b)`: Return a random integer `N` such that `a <= N <= b`.
    3. `random.random()`: Return the next random floating point number in the range `[0.0, 1.0)`.
    4. Return a random element from a list
      * `pick = int(random.random() * len(array))`
      * `array[random.randint(0, len(array)-1)]`
      * `random.choice(array)`
    5. Do something with `k/i` probability: `random.random() < k/i`, where `k <= i`


3. If an array of length `n` has `n!` distinct permutations. Therefore, in order to encode all permutations in an integer space, `⌈lg(n!)⌉` bits are necessary, which may not be guaranteed by the default PRNG (pseudorandom number generators).

4. [Shuffle an array randomly][LC384. Shuffle an Array]
  1.  The brute force algorithm essentially puts each number in a "hat", and draws them at random (without replacement) until there are none left. `O(n^2)`
    * Mechanically, this is performed by copying the contents of array into a second auxiliary array named aux before overwriting each element of array with a randomly selected one from aux. After selecting each random element, it is removed from aux to prevent duplicate draws `O(n)`. The implementation of reset is simple, as we just store the original state of nums on construction.
    * Therefore, no matter on which draw an element is drawn, it is drawn with a `\frac{1}{n}` chance, so each array permutation is equally likely to arise.
  2. Fisher-Yates Algorithm: `O(n)`
    * by swapping elements around within the array itself, we can avoid the linear space cost of the auxiliary array and the linear time cost of list modification.
    * On each iteration of the algorithm, we generate a random integer between the current index and the last index of the array. 
    * Then, we swap the elements at the current index and the chosen index - this simulates drawing (and removing) the element from the hat, as the next range from which we select a random index will not include the most recently processed one. 
    * One small, yet important detail is that it is possible to swap an element with itself - otherwise, some array permutations would be more likely than others. 
  3. Python built-in `random.shuffle(array)`, shuffles the array in-place, `O(n)`

5. Sampling with weight
  1. [LC528. Random Pick with Weight][LC528. Random Pick with Weight]

6. 洗牌算法
  1. 分析洗牌算法正确性的准则：产生的结果必须有 n! 种可能，否则就是错误的。
  ```
  // 得到一个在闭区间 [min, max] 内的随机整数
  int randInt(int min, int max);

  // 第一种写法
  void shuffle(int[] arr) {
      int n = arr.length();
      /******** 区别只有这两行 ********/
      for (int i = 0 ; i < n; i++) {
          // 从 i 到最后随机选一个元素
          int rand = randInt(i, n - 1);
          /*************************/
          swap(arr[i], arr[rand]);
      }
  }

  // 第二种写法
      for (int i = 0 ; i < n - 1; i++)
          int rand = randInt(i, n - 1);

  // 第三种写法
      for (int i = n - 1 ; i >= 0; i--)
          int rand = randInt(0, i);

  // 第四种写法
      for (int i = n - 1 ; i > 0; i--)
          int rand = randInt(0, i);

  ```

2. 蒙特卡罗方法验证正确性
  1. 随机乱置算法的正确性衡量标准是：对于每种可能的结果出现的概率必须相等，也就是说要足够随机。
  2. 第一种思路，我们把数组 arr 的所有排列组合都列举出来，做成一个直方图（假设 arr = {1,2,3}）, 每次进行洗牌算法后，就把得到的打乱结果对应的频数加一，重复进行 100 万次，如果每种结果出现的总次数差不多，那就说明每种结果出现的概率应该是相等的。
  3. 第二种思路，可以这样想，arr 数组中全都是 0，只有一个 1。我们对 arr 进行 100 万次打乱，记录每个索引位置出现 1 的次数，如果每个索引出现 1 的次数差不多，也可以说明每种打乱结果的概率是相等的。

[LC382. Linked List Random Node]: https://leetcode.com/problems/linked-list-random-node/
[LC384. Shuffle an Array]: https://leetcode.com/problems/shuffle-an-array/
[LC528. Random Pick with Weight]: https://leetcode.com/problems/random-pick-with-weight/
[Reservoir Sampling]: https://florian.github.io/reservoir-sampling/
[洗牌算法详解]: 