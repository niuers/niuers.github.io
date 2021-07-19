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

1. [The module `heapq` in Python standard library][Python heapq Heap Queue Algorithm] provides an implementation of the **min heap queue**, also known as priority queue algorithm. 
    ```
    Usage:
    heap = []            # creates an empty heap
    heappush(heap, item) # pushes a new item on the heap
    item = heappop(heap) # pops the smallest item from the heap
    #Note. Don't use the list's pop() function, i.e. heap.pop() here, it will return the items from last to beginning, not neccesarrily in order.
    item = heap[0]       # smallest item on the heap without popping it
    #Note. there's NO guarantee that the elements after heap[0] are ordered, only that heap[0] is the smallest item
    
    # heapify transforms list into a heap, in-place, in linear time O(n). In the resulting heap the smallest element gets pushed to the index position 0. But rest of the data elements are not necessarily sorted.
    heapify(x)           
    
    item = heapreplace(heap, item) # pops and returns smallest item, and adds
                                # new item; the heap size is unchanged
    ```

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

10. `nlargest() and nsmallest()`: `O(n+klog(k,2))`

11. Apply a custom comparison function to the items in the priority queue
```
# Use a class and overwrite the __lt__() function

class Node:
    def __init__(self, word, freq):
        self.word = word
        self.freq = freq
    
    def __repr__(self):
        return f"({self.word, self.freq})"
    def __lt__(self, other):
        if self.freq < other.freq:
            return True
        elif self.freq > other.freq:
            return False
        
        return self.word >= other.word

hq = []
for w, f in word_freq.items():
    heappush(hq, Node(word, freq))        
```





[Python heapq Heap Queue Algorithm]: https://docs.python.org/3/library/heapq.html