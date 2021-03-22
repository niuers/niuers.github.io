---
title: "Python Priority Queue: A Complete Picture"
date: 2021-03-22
categories:
  - blog
tags:
  - python
  - priority queue
  - heap queue
---

1. [The module `heapq` in Python standard library][Python heapq Heap Queue Algorithm] provides an implementation of the min heap queue, also known as priority queue algorithm. 

2. Push an item onto the heap:
    * `heappush`: `O(log(n))`

3. Pop and return **the smallest item** from the heap
    * `heappop`: `O(log(n))`

4. Fetch **the smallest item** from the heap without pop
    * `heap[0]`: `O(1)`

5. To get a **max heap**:
    * Push the negative of the value into the heap

6. How to keep sort stability? 
    * How do you get two tasks with equal priorities to be returned in the order they were originally added?
    * Tuple comparison breaks for `(priority, task)` pairs if the priorities are equal and the tasks do not have a default comparison order.
    * Solution: store entries as 3-element list including the `priority`, `an entry count`, and `the task`. The entry count serves as a tie-breaker so that two tasks with the same priority are returned in the order they were added. 

7. If the priority of a task changes, how do you move it to a new position in the heap? Or if a pending task needs to be deleted, how do you find it and remove it from the queue?
    * Finding a task can be done with a dictionary pointing to an entry in the queue.
    * Removing the entry or changing its priority is more difficult because it would break the heap structure invariants. So, a possible solution is to mark the entry as removed and add a new entry with the revised priority
    * This results in `O(log(n))` time complexity for removal.

8. Here's the template provided by Python document

    ```
    pq = []                         # list of entries arranged in a heap
    entry_finder = {}               # mapping of tasks to entries
    REMOVED = '<removed-task>'      # placeholder for a removed task
    counter = itertools.count()     # unique sequence count

    def add_task(task, priority=0):
        'Add a new task or update the priority of an existing task'
        if task in entry_finder:
            remove_task(task)
        count = next(counter)
        entry = [priority, count, task]
        entry_finder[task] = entry
        heappush(pq, entry)

    def remove_task(task):
        'Mark an existing task as REMOVED.  Raise KeyError if not found.'
        entry = entry_finder.pop(task)
        entry[-1] = REMOVED

    def pop_task():
        'Remove and return the lowest priority task. Raise KeyError if empty.'
        while pq:
            priority, count, task = heappop(pq)
            if task is not REMOVED:
                del entry_finder[task]
                return task
        raise KeyError('pop from an empty priority queue')

    ```

9. Heap sort is `O(nlog(n))`









[Python heapq Heap Queue Algorithm]: https://docs.python.org/3/library/heapq.html