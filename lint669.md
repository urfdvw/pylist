# [669. Coin Change](https://www.lintcode.com/problem/coin-change/description?_from=ladder&&fromId=92)

You are given coins of different denominations and a total amount of money amount. Write a function to compute the fewest number of coins that you need to make up that amount. If that amount of money cannot be made up by any combination of the coins, return -1.

You may assume that you have an infinite number of each kind of coin.

Example1
```
Input: 
[1, 2, 5]
11
Output: 3
Explanation: 11 = 5 + 5 + 1
```
Example2
```
Input: 
[2]
3
Output: -1
```

## Solution
```python
class Solution:
    """
    @param coins: a list of integer
    @param amount: a total amount of money amount
    @return: the fewest number of coins that you need to make up
    """
    def coinChange(self, coins, amount):
        # dp[i][y] stands for the min number of coins needed, -1 if not possible
        # first i coins considered
        # amount y
        dp = [[-1]*(amount+1) for i in range(len(coins)+1)]
        dp[0][0] = 0
        for i in range(1, len(coins)+1):
            for y in range(amount+1):
                if y < coins[i-1]:
                    dp[i][y] = dp[i-1][y]
                else:
                    dp[i][y] = self.min_or(
                        dp[i-1][y], 
                        self.add1(dp[i][y-coins[i-1]])
                        )
        return dp[-1][-1]
    def add1(self, a):
        if a == -1:
            return -1
        return a + 1
    def min_or(self, a, b):
        if a == -1:
            return b
        if b == -1:
            return a
        return min([a, b])
```
## special care
- ```-1``` is very special key, so min and add operation are redefined
- 这个题的运算相当于最小值和可行性的叠加运算
    - 运算本身被定义在```min_or```里面，仍然符合交换律和结合律
    - 因为是叠加运算所以update过程也要特别处理，放在```add1```函数里面