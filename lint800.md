# [800. Backpack IX](https://www.lintcode.com/problem/backpack-ix/description?_from=ladder&&fromId=92)

You have a total of n thousand yuan, hoping to apply for a university abroad. The application is required to pay a certain fee. Give the cost of each university application and the probability of getting the University's offer, and the number of university is m. If the economy allows, you can apply for multiple universities. Find the highest probability of receiving at least one offer.

0<=n<=10000,0<=m<=10000

Example 1:
```
Input:  
    n = 10
    prices = [4,4,5]
    probability = [0.1,0.2,0.3]
Output:  0.440

Explanation：
select the second and the third school. 
```

Example 2:
```
Input: 
    n = 10
    prices = [4,5,6]
    probability = [0.1,0.2,0.3]
Output:  0.370

Explanation:
select the first and the third school.`
```

## Solutions
```python
class Solution:
    """
    @param n: Your money
    @param prices: Cost of each university application
    @param probability: Probability of getting the University's offer
    @return: the  highest probability
    """
    def backpackIX(self, n, prices, probability):
        # variable to store answers
        # dp[i][y] is the answer of questions:
        #   find the prob. of get at least 1 offer
        #   first i schools, i = 0 : len(prices)
        #   with available money y, y = 0 : n
        dp = [[0]*(1+n) for i in range(2)]
        # dp[0]: no prob, keep as is
        # dp[1] ~ dp[-1]
        for i in range(1, len(prices)+1):
            for y in range(1, n+1):
                if y < prices[i-1]:
                    dp[i%2][y] = dp[(i-1)%2][y]
                else:
                    dp[i%2][y] = max([
                        dp[(i-1)%2][y], # not apply
                        self.prob_add(probability[i-1], dp[(i-1)%2][y-prices[i-1]])
                        ])
        return float(dp[len(prices)%2][-1]) # f*** 
        
    def prob_add(self, p1, p2):
        return 1 - (1-p1) * (1-p2)
```
## note
- 自定义的函数也符合交换律和结合律