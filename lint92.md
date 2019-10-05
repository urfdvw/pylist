# [92. Backpack](https://www.lintcode.com/problem/backpack/description)

Given n items with size Ai, an integer m denotes the size of a backpack. How full you can fill this backpack?

You can not divide any item into small pieces.

Example 1:
```
	Input:  [3,4,8,5], backpack size=10
	Output:  9
```
Example 2:
```
	Input:  [2,3,5,7], backpack size=12
	Output:  12
```
Challenge
```
O(n x m) time and O(m) memory.

O(n x m) memory is also acceptable if you do not know how to optimize memory.
```
## Solution
The following solution consider the question **whether you can fill the backpack or not** and return the largest backpack in the last row that can be filled.
```python
class Solution:
    """
    @param m: An integer m denotes the size of a backpack
    @param A: Given n items with size A[i]
    @return: The maximum size
    """
    def backPack(self, m, A):
        # dp[i][y]: bool, true if 
        # backpack with size Y can be fully filled with 
        # first i items
        dp = [[False]*(m+1) for i in range(len(A)+1)]
        dp[0][0] = True
        for i in range(1, len(A)+1) :
            dp[i][0] = True
            for y in range(1, m+1):
                if y < A[i-1]:
                    dp[i][y] = dp[i-1][y]
                else:
                    dp[i][y] = dp[i-1][y] or dp[i-1][y-A[i-1]]
        j = len(dp[0]) - 1
        while j >= 0:
            if dp[-1][j]:
                return j
            else:
                j -= 1
```
Or directly look for the maximum volume filled for each backpack size.
```python
class Solution:
    """
    @param m: An integer m denotes the size of a backpack
    @param A: Given n items with size A[i]
    @return: The maximum size
    """
    def backPack(self, m, A):
        # dp[i][y] is the maximum volum occupied with
        # first i items considered and
        # backpack size y
        dp = [[0]*(m+1) for i in range(len(A)+1)]
        for i in range(1, len(A)+1):
            for y in range(1+m):
                if y < A[i-1]:
                    dp[i][y] = dp[i-1][y]
                else:
                    dp[i][y] = max([
                        dp[i-1][y],
                        dp[i-1][y-A[i-1]] + A[i-1]
                    ])
        return dp[-1][-1]
```
## optimization
- rotation arrays can be used