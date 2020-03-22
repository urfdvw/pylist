# [40. Implement Queue by Two Stacks](https://www.lintcode.com/problem/implement-queue-by-two-stacks/description)

As the title described, you should only use two stacks to implement a queue's actions.

The queue should support push(element), pop() and top() where pop is pop the first(a.k.a front) element in the queue.

Both pop and top methods should return the value of first element.

Example 1:
```
Input:
    push(1)
    pop()    
    push(2)
    push(3)
    top()    
    pop()     
Output:
    1
    2
    2
```
Example 2:
```
Input:
    push(1)
    push(2)
    push(2)
    push(3)
    push(4)
    push(5)
    push(6)
    push(7)
    push(1)
Output:
[]
```
Challenge
```
implement it by two stacks, do not use any other data structure and push, pop and top should be O(1) by AVERAGE.
```
Notice
```
Suppose the queue is not empty when the pop() function is called.
```
# Solution
```python
class MyQueue:
    
    def __init__(self):
        self.push_stack = []
        self.pop_stack = []
        self.last = None

    """
    @param: element: An integer
    @return: nothing
    """
    def push(self, element):
        while len(self.pop_stack) > 0:
            self.push_stack.append(self.pop_stack.pop())
        self.push_stack.append(element)

    """
    @return: An integer
    """
    def pop(self):
        while len(self.push_stack) > 0:
            self.pop_stack.append(self.push_stack.pop())
        return self.pop_stack.pop()

    """
    @return: An integer
    """
    def top(self):
        while len(self.push_stack) > 0:
            self.pop_stack.append(self.push_stack.pop())
        return self.pop_stack[-1]
```