# [428. Pow(x, n)](https://www.lintcode.com/problem/powx-n/description)

Implement pow(x, n). (n is an integer.)

You don't need to care about the precision of your answer, it's acceptable if the expected answer and your answer 's difference is smaller than 1e-3.

Example 1:
```
Input: x = 9.88023, n = 3
Output: 964.498
```
Example 2:
```
Input: x = 2.1, n = 3
Output: 9.261
```
Example 3:
```
Input: x = 1, n = 0
Output: 1
```

# Solution
```python
class Solution:
    """
    in:
        n: int
    out:
        b: list of ints right is significant
    """
    def int_2_binarylist(self, n):
        m = n
        b = []
        while m > 0:
            m, r = divmod(m, 2)
            b.append(r)
        return b
        
    """
    @param x {float}: the base number
    @param n {int}: the power number
    @return {float}: the result
    """
    def myPowPositive(self, x, n):
        # convert n to b
        b = self.int_2_binarylist(n)
        # 
        power_x = x
        ans = 1
        for bit in b:
            if bit :
                ans *= power_x
            power_x *= power_x
        return ans
    
    def myPow(self, x, n):
        if n >= 0:
            return self.myPowPositive(x, n)
        else:
            return 1 / self.myPowPositive(x, -n)
```
# test case:
- n=0
- n=1
# special care
- n can be negative