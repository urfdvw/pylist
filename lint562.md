# [562. Backpack IV](https://www.lintcode.com/problem/backpack-iv/description?_from=ladder&&fromId=92)

Given an integer array nums[] which contains n unique positive numbers, num[i] indicate the size of ith item. An integer target denotes the size of backpack. Find the number of ways to fill the backpack.

Each item may be chosen unlimited number of times

Example1
```
Input: nums = [2,3,6,7] and target = 7
Output: 2
Explanation:
Solution sets are: 
[7]
[2, 2, 3]
```
Example2
```
Input: nums = [2,3,4,5] and target = 7
Output: 3
Explanation:
Solution sets are: 
[2, 5]
[3, 4]
[2, 2, 3]
```
## Solutions

```python
class Solution:
    """
    @param nums: an integer array and all positive numbers, no duplicates
    @param m: An integer
    @return: An integer
    """
    def backPackIV(self, nums, m):
        # dp[i][y] means the number of ways to fill the backpack
        # when first i items are considered
        # and backpack size y
        dp = [[0]*(m+1) for i in range(len(nums)+1)]
        dp[0][0] = 1
        for i in range(1, len(nums)+1):
            for y in range(m+1):
                if y < nums[i-1]:
                    dp[i][y] = dp[i-1][y]
                else:
                    dp[i][y] = dp[i][y-nums[i-1]] + dp[i-1][y]
        return dp[-1][-1]
```