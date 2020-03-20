# [140. Fast Power](https://www.lintcode.com/problem/fast-power/description)
Calculate the a^n%b where a, b and n are all 32bit non-negative integers.

Example
```
For 2^31 % 3 = 2

For 100^1000 % 1000 = 0
```
# Solution
```python
class Solution:
    """
    @param a: A 32bit integer
    @param b: A 32bit integer
    @param n: A 32bit integer
    @return: An integer
    """
    def fastPower(self, a, b, n):
        if n == 0:
            return 1 % b
        
        # convert n to b
        bits = self.int_2_binarylist(n)
        # 
        power_a = a % b
        r = None
        for bit in bits:
            if bit :
                if r is None:
                    # if first computation
                    r = power_a % b
                else:
                    # update r
                    r = (r * power_a) % b
            power_a = power_a * power_a % b
        return r

    """
    in:
        n: int
    out:
        b: list of bool:
            n = sum_{i=0}^{len(b)-1} 2^b[i]
    """
    def int_2_binarylist(self, n):
        m = n
        b = []
        while m > 0:
            m, r = divmod(m, 2)
            b.append(r)
        return b
```
# math
- ak % b = (a % b)(k % b)

# question
- Q: can n be negative ?
    - A: No.