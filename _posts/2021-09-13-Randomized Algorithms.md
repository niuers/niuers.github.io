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
        #   from the inclusive range {a, ..., b} *)
        j := randomInteger(1, i)
        if j <= k
            R[j] := S[i]
    ```
    * Step 1: Store the first `k` elements.
    * Step 2: Every time we see the `ith` element we select to keep it with `k/i` probability. If the element is selected then we randomly knock off any one of the already existing `k` elements in the storage uniformly (with probability `1/k`) and replace it with the selected element.
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


[LC382. Linked List Random Node]: https://leetcode.com/problems/linked-list-random-node/
[LC384. Shuffle an Array]: https://leetcode.com/problems/shuffle-an-array/