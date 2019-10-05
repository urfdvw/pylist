# [125. Backpack II](https://www.lintcode.com/problem/backpack-ii/description?_from=ladder&&fromId=92)

There are n items and a backpack with size m. Given array A representing the size of each item and array V representing the value of each item.

What's the maximum value can you put into the backpack?

A[i], V[i], n, m are all integers.
You can not split an item.
The sum size of the items you want to put into backpack can not exceed m.
Each item can only be picked up once

Example 1:
```
Input: m = 10, A = [2, 3, 5, 7], V = [1, 5, 2, 4]
Output: 9
Explanation: Put A[1] and A[3] into backpack, getting the maximum value V[1] + V[3] = 9 
```
Example 2:
```
Input: m = 10, A = [2, 3, 8], V = [2, 5, 8]
Output: 10
Explanation: Put A[0] and A[2] into backpack, getting the maximum value V[0] + V[2] = 10 
```
Challenge
```
O(nm) memory is acceptable, can you do it in O(m) memory?
```
## Solution
```python
class Solution:
    """
    @param m: An integer m denotes the size of a backpack
    @param A: Given n items with size A[i]
    @param V: Given n items with value V[i]
    @return: The maximum value
    """
    def backPackII(self, m, A, V):
        # variable to store answers
        # dp[i][y] is the answer of questions:
        #   find the max value of
        #   first i items, i = 0 : len(A)
        #   with backpack size y, y = 0 : m
        dp = [[0]*(m+1) for i in range(len(A)+1)]
        # first row, just keek it zero
        # for the second to the last row
        for i in range(1, 1+len(A)):
            for y in range(1, 1+m):
                if y < A[i-1]:  # if backpack size smaller than item
                    dp[i][y] = dp[i-1][y]
                else:
                    dp[i][y] = max([
                        dp[i-1][y],  # not include item i-1
                        V[i-1] + dp[i-1][y-A[i-1]] # include
                        ])
        return dp[-1][-1]
```