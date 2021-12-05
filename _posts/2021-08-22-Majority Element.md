---
title: "Majority Element"
date: 2021-08-22
categories:
  - blog
tags:
  - algorithm
  - summary
---

1. Find the majority element in an array
    1. It relates to fault-tolerant computing. One performs multiple redundant computations and then verify that a majority of the results agree.
    2. Boyer-Moore voting Algorithm: `O(n)` in time and `O(1)` in space.
        * With 1 counter, you can cancel (pair) half of the numbers (at some place where counter == 0), so the majority in the rest of the numbers is still majority.
        * With 2 counters, you can cancel (pair) `1/3` of the numbers (at some place where counter == 0), so the majority in the rest of the numbers is still majority.

2. Find the element(s) that has at least `int(n/3)` in an array



[LC]: 