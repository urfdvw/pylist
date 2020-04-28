# [155. Min Stack](https://leetcode.com/problems/min-stack/)

Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

- push(x) -- Push element x onto stack.
- pop() -- Removes the element on top of the stack.
- top() -- Get the top element.
- getMin() -- Retrieve the minimum element in the stack.
 

Example 1:

    Input
    ["MinStack","push","push","push","getMin","pop","top","getMin"]
    [[],[-2],[0],[-3],[],[],[],[]]

    Output
    [null,null,null,null,-3,null,0,-2]

    Explanation
    MinStack minStack = new MinStack();
    minStack.push(-2);
    minStack.push(0);
    minStack.push(-3);
    minStack.getMin(); // return -3
    minStack.pop();
    minStack.top();    // return 0
    minStack.getMin(); // return -2
 

Constraints:

    Methods pop, top and getMin operations will always be called on non-empty stacks.

# Solution
Stack Solution
```python
class MinStack:

    def __init__(self):
        self.data = []
        self.min = []
        
    def push(self, x: int) -> None:
        self.data.append(x)
        
        if len(self.min) == 0:
            self.min.append(x)
            return
        
        if x <= self.min[-1]: # = for multiple same value
            self.min.append(x)
            return
        
    def pop(self) -> None:
        out = self.data.pop()
        if out == self.min[-1]:
            self.min.pop()
        return out
    
    def top(self) -> int:
        return self.data[-1]
        
    def getMin(self) -> int:
        return self.min[-1]
```

# Care
- 不要把attribute和method起同一个名字
- 用`a[0]`作为peek之前一定先判断list是否为空
- 不要在某些语句的末尾加入无意义的冒号
    - 只要注意缩紧这个其实很容易避免

# Not suggested solution
heap + trash list solution
```python
from heapq import heappush, heappop
class MinStack:

    def __init__(self):
        self.stack = []
        self.heap = []
        self.poped = set()
        

    def push(self, x: int) -> None:
        self.stack.append(x)
        heappush(self.heap, x)
        

    def pop(self) -> None:
        out = self.stack.pop()
        self.poped.add(out)
        while len(self.heap) > 0 and self.heap[0] in self.poped:
            self.poped.remove(heappop(self.heap))
        return out
    
    def top(self) -> int:
        return self.stack[-1]
        

    def getMin(self) -> int:
        return self.heap[0]
```