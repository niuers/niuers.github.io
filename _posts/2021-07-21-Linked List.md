---
title: "Linked List"
date: 2021-07-21
categories:
  - blog
tags:
  - algorithm
  - leetcode
  - Linked List
  - summary
---

1. We can add an auxiliary "sentinel" node, which points to the list head. The "sentinel" node is used to simplify some corner cases such as a list with only one node, or removing the head of the list. In such case, you may return `sentinel.next` as new head in case the original `head` has been changed.

2. To goto the middle of a linked list, you can use a slow and a fast pointers, where the fast pointer moves two steps each time, while the slow pointer moves one step each time.

3. If you want to achieve constant space with some linked list problems (Usually required), you can try put the results together with the original linked list, for example, interleaving old and new nodes in the same list.

4. Floyd's Tortoise and Hare Cycle Finding Algorithm
    * Since the speed difference is 1, it takes `{distance between the 2 runners}/{difference of speed}` iterations for the fast runner to catch up with the slow runner.
    * Floyd's algorithm is separated into two distinct phases. In the first phase, it determines whether a cycle is present in the list. If no cycle is present, it returns null immediately, as it is impossible to find the entrance to a nonexistant cycle. Otherwise, it uses the located "intersection node" to find the entrance to the cycle.
        * Here, we initialize two pointers - the fast hare and the slow tortoise. Then, until hare can no longer advance, we increment tortoise once and hare twice. If, after advancing them, hare and tortoise point to the same node, we return it. Otherwise, we continue. If the while loop terminates without returning a node, then the list is acyclic, and we return null to indicate as much.
            * Here, the nodes in the cycle have been labelled from `0` to `C-1`, where `C` is the length of the cycle. The noncyclic nodes have been labelled from `-F` to `-1`, where `F` is the number of nodes outside of the cycle. The start of the cycle has label `0`.
            * Suppose the intersection node is `h` from the start of cycle `0`, since hare travels twice as much as tortoise(`d(tortoise)=(F+h)`, tortoise must meet with hare before it travels the full cycle for the first time.), we have `d(hare)=2*d(tortoise) = 2*(F+h) = F + (F+2h)`, consider the distance after hare goes into the cycle and stays at position `h`, we have `F+2h % C = h`, i.e. `F=kC-h`.            
        * Given that phase 1 finds an intersection, phase 2 proceeds to find the node that is the entrance to the cycle. To do so, we initialize two more pointers: ptr1, which points to the head of the list, and ptr2, which points to the intersection. Then, we advance each of them by 1 until they meet; the node where they meet is the entrance to the cycle, so we return it.
            * Now if we move `F` steps from the intersection point `h`, we will have hare (now moves 1 step each time) moves to the start of cycle. This is because `h+F=h+(kC-h)=kC`, which goes to node `0`.
            * At the same time, pointer `ptr1` moves `F` steps as well, which will stops at node `0`, so when they meet, the node `0` is found.
    * Problems
        * [LC142. Linked List Cycle II][LC142. Linked List Cycle II]

5. Mix a linked list
    1. We can save the node pointers to an array, and use that for mixing
    2. Or we can find the middle part of the list, reverse the 2nd part, and merge two lists, so we can have `O(1)` space

6. In order to insert a new element into a singly-linked list, we apply a trick.
    * The idea is that we use a pair of pointers (namely `prev -> next`) which serve as place-holders to guard the position where in-between we would insert a new element (i.e. `prev -> new_node -> next`).
    * Problems
        * [LC147. Insertion Sort List][LC147. Insertion Sort List]

7. Sort a list
    * If you use bottom-up merge sort, the space is `O(1)`. The solution is to use the size of the list, and do sort on the size of 1,2,,4,8,16..., then merge neighbor lists.

8. [Circular Linked List][LC708. Insert into a Sorted Circular Linked List]
    * Try two pointers
9. Reverse a linked list
    * Insert the node one-by-one in the proper order for the reversed list
    

[LC142. Linked List Cycle II]: https://leetcode.com/problems/linked-list-cycle-ii/
[LC147. Insertion Sort List]: https://leetcode.com/problems/insertion-sort-list/
[LC148. Sort List]: https://leetcode.com/problems/sort-list/
[LC708. Insert into a Sorted Circular Linked List]: https://leetcode.com/problems/insert-into-a-sorted-circular-linked-list/


    


