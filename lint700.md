# [700. Cutting a Rod](https://www.lintcode.com/problem/cutting-a-rod/description?_from=ladder&&fromId=92)

Given a rod of length n inches and an array of prices that contains prices of all pieces of size smaller than n. Determine the maximum value obtainable by cutting up the rod and selling the pieces.

Example1
```
Input:
[1, 5, 8, 9, 10, 17, 17, 20]
8
Output: 22
Explanation:
length   | 1   2   3   4   5   6   7   8  
--------------------------------------------
price    | 1   5   8   9  10  17  17  20
by cutting in two pieces of lengths 2 and 6
```
Example2
```
Input:
[3, 5, 8, 9, 10, 17, 17, 20]
8
Output: 24
Explanation:
length   | 1   2   3   4   5   6   7   8  
--------------------------------------------
price    | 3   5   8   9  10  17  17  20
by cutting in eight pieces of length 1.
```

## Solution
```python
class Solution:
    """
    @param prices: the prices
    @param n: the length of rod
    @return: the max value
    """
    def cutting(self, prices, n):
        # dp[i][y] is the maximun value acquired for
        # first i items concidered
        # with length n
        dp = [[0]*(n+1) for i in range(len(prices)+1)]
        for i in range(1, len(prices)+1):
            for y in range(n+1):
                if y < i:
                    dp[i][y] = dp[i-1][y]
                else:
                    dp[i][y] = max([
                        dp[i-1][y],
                        dp[i][y - i] + prices[i - 1]
                        ])
        return dp[-1][-1]
```
## special care
- ```size[i-1]``` is actually ```i```