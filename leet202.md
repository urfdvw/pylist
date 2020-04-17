# [202. Happy Number](https://leetcode.com/problems/happy-number/)

Write an algorithm to determine if a number n is "happy".

A happy number is a number defined by the following process: Starting with any positive integer, replace the number by the sum of the squares of its digits, and repeat the process until the number equals 1 (where it will stay), or it loops endlessly in a cycle which does not include 1. Those numbers for which this process ends in 1 are happy numbers.

Return True if n is a happy number, and False if not.

Example: 

    Input: 19
    Output: true
    Explanation: 
    1^2 + 9^2 = 82
    8^2 + 2^2 = 68
    6^2 + 8^2 = 100
    1^2 + 0^2 + 0^2 = 1

# Solution
compute then add
```python
class Solution:
    def isHappy(self, n: int) -> bool:
        record = set([n])
        while True:
            n = self.convert(n)
            if n == 1:
                return True
            if n in record:
                return False
            record.add(n)
        
    def convert(self, n: int) -> int:
        ans = 0
        while n >= 10:
            ans += (n % 10) * (n % 10)
            n = n // 10
        ans += (n % 10) * (n % 10)
        return ans
```


add then compute
```python
class Solution:
    def isHappy(self, n: int) -> bool:
        record = set()
        while True:
            if n == 1:
                return True
            if n in record:
                return False
            record.add(n)
            n = self.convert(n)
        
    def convert(self, n: int) -> int:
        ans = 0
        while n >= 10:
            ans += (n % 10) * (n % 10)
            n = n // 10
        ans += (n % 10) * (n % 10)
        return ans
        
```
