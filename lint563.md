# [563. Backpack V](https://www.lintcode.com/problem/backpack-v/description?_from=ladder&&fromId=92)

Given n items with size nums[i] which an integer array and all positive numbers. An integer target denotes the size of a backpack. Find the **number of possible ways** fill the backpack.

Each item may only be used once

Example

```
Given candidate items [1,2,3,3,7] and target 7,

A solution set is: 
[7]
[1, 3, 3]
return 2
```
## Solution
```python
class Solution:
    """
    @param nums: an integer array and all positive numbers
    @param target: An integer
    @return: An integer
    """
    def backPackV(self, A, m):
        # variable to store answers
        # dp[i][y] is the answer of questions:
        #   find the number of ways to fill the backpack
        #   first i items, i = 0 : len(A)
        #   with backpack size y, y = 0 : m
        dp = [[0]*(m+1) for i in range(2)]
        # first row, zero fill zero
        dp[0][0] = 1
        # for the second to the last row
        for i in range(1, 1+len(A)):
            dp[i % 2][0] = 1 # zero is always able to be filled
            for y in range(1, 1+m):
                if y < A[i-1]:  # if backpack size smaller than item
                    dp[i % 2][y] = dp[(i-1) % 2][y]
                else:
                    dp[i % 2][y] = dp[(i-1) % 2][y] + dp[(i-1) % 2][y-A[i-1]] # include
        return dp[len(A) % 2][-1]
```