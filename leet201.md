# [201. Bitwise AND of Numbers Range](https://leetcode.com/problems/bitwise-and-of-numbers-range/)

Given a range [m, n] where 0 <= m <= n <= 2147483647, return the bitwise AND of all numbers in this range, inclusive.

Example 1:

    Input: [5,7]
    Output: 4
Example 2:

    Input: [0,1]
    Output: 0

# Solution
```python
class Solution:
    def rangeBitwiseAnd(self, m: int, n: int) -> int:
        mb = self.D2B(m)
        nb = self.D2B(n)
        
        if len(nb) != len(mb):
            return 0
        
        ans = 0
        for i in range(len(mb)-1, -1, -1):
            if mb[i] == nb[i]:
                if mb[i] == 1:
                    ans += 2 ** i
            else:
                break
        return ans
        
    def D2B(self, m):
        ans = []
        while m > 0:
            ans.append(m % 2)
            m = m // 2
        return ans
```
```steps
```