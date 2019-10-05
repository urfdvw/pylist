# [801. Backpack X](https://www.lintcode.com/problem/backpack-x/description?_from=ladder&&fromId=92)

You have a total of n yuan. Merchant has three merchandises and their prices are 150 yuan, 250 yuan and 350 yuan. And the number of these merchandises can be considered as infinite. After the purchase of goods need to be the remaining money to the businessman as a tip, finding the minimum tip for the merchant.

Example 1:
```
Input:  n = 900
Output:  0
```
Example 2:
```
Input:  n = 800
Output:  0
```
## Solutions
```python
class Solution:
    """
    @param n: the money you have
    @return: the minimum money you have to give
    """
    def backPackX(self, n):
        m = n // 50
        prices = [3, 5, 7]
        # dp[i][y]
        # maximun money spent
        # first i items are considered
        # y is money/50 can use
        dp = [[0]*(m+1) for i in range(len(prices)+1)]
        for i in range(1, len(prices)+1):
            for y in range(m+1):
                if y < prices[i-1]:
                    dp[i][y] = dp[i-1][y]
                else:
                    dp[i][y] = max([dp[i-1][y], prices[i-1] + dp[i][y-prices[i-1]]])
        return n - 50*dp[-1][-1]
```
## Note
- 用最大公约数的倍数可以减少无用的搜索，问题本身的大小变成了 ```m = n // 50```，最后记得转换回来就是了。