# [642. Moving Average from Data Stream](lintcode.com/problem/moving-average-from-data-stream/description)

Given a stream of integers and a window size, calculate the moving average of all integers in the sliding window.

Example 1:
```
MovingAverage m = new MovingAverage(3);
m.next(1) = 1 // return 1.00000
m.next(10) = (1 + 10) / 2 // return 5.50000
m.next(3) = (1 + 10 + 3) / 3 // return 4.66667
m.next(5) = (10 + 3 + 5) / 3 // return 6.00000
```
# solution
```python
from collections import deque
class MovingAverage:
    """
    @param: size: An integer
    """
    def __init__(self, size):
        self.q = deque()
        self.size = size
        self.sum = 0

    """
    @param: val: An integer
    @return:  
    """
    def next(self, val):
        self.q.append(val)
        self.sum += val
        if len(self.q) > self.size:
            self.sum -= self.q.popleft()
        return self.sum / len(self.q)
        
# Your MovingAverage object will be instantiated and called as such:
# obj = MovingAverage(size)
# param = obj.next(val)
```