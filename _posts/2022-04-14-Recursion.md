---
title: "Recursion"
date: 2022-04-14
categories:
  - blog
tags:
  - algorithm
  - summary
  - recursion
---

1. Time Complexity for Recursion Problems
    1. 递归算法的时间复杂度怎么计算？
        1. 就是用子问题个数乘以解决一个子问题需要的时间
        2. 子问题个数，即递归树中节点的总数
    2. [所有递归的算法，你甭管它是干什么的，本质上都是在遍历一棵（递归）树，然后在节点（前中后序位置）上执行代码，你要写递归算法，本质上就是要告诉每个节点需要做什么。][归并排序详解及应用]
2. How to Debug Recursion Algorithm?
    1. 直接在递归函数内部打印关键值，配合缩进，直观地观察递归函数执行情况
    ```
    // 全局变量，记录递归函数的递归层数
    int count = 0;

    // 输入 n，打印 n 个 tab 缩进
    void printIndent(int n) {
        for (int i = 0; i < n; i++) {
            printf("   ");
        }
    }
    ```

    2. 在递归函数的开头，调用 printIndent(count++) 并打印关键变量；然后在所有 return 语句之前调用 printIndent(--count) 并打印返回值。
    3. 就是在函数开头和所有 return 语句对应的地方加上一些打印代码。
    4. 最重要的是，这样可以比较直观地看出递归过程，你有没有发现这就是一棵递归树？







[归并排序详解及应用]: https://labuladong.github.io/algo/2/19/38/
    





