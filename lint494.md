# [494. Implement Stack by Two Queues](https://www.lintcode.com/problem/implement-stack-by-two-queues/description)

Implement a stack by two queues. The queue is first in first out (FIFO). That means you can not directly pop the last element in a queue.

Example 1:
```
Input:
push(1)
pop()
push(2)
isEmpty() // return false
top() // return 2
pop()
isEmpty() // return true
```
Example 2:
```
Input:
isEmpty()
```

# solution
```python
from collections import deque
class Stack:
    def __init__(self):
        self.q = [deque() for i in range(2)]
        self.cur = 0
        self.last = None
    """
    @param: x: An integer
    @return: nothing
    """
    def push(self, x):
        self.q[self.cur].append(x)
        self.last = x

    """
    @return: nothing
    """
    def pop(self):
        while len(self.q[self.cur]) > 1:
            self.last = self.q[self.cur].popleft()
            self.q[1 - self.cur].append(self.last)
        out = self.q[self.cur].popleft()
        self.cur = 1 - self.cur
        return out

    """
    @return: An integer
    """
    def top(self):
        return self.last

    """
    @return: True if the stack is empty
    """
    def isEmpty(self):
        return len(self.q[self.cur]) == 0
```