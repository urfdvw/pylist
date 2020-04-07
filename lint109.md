# [109. Triangle](https://www.lintcode.com/problem/triangle/description)

Given a triangle, find the minimum path sum from top to bottom. Each step you may move to adjacent numbers on the row below.


Example 1:
```
Input the following triangle:
[
     [2],
    [3,4],
   [6,5,7],
  [4,1,8,3]
]
Output: 11
Explanation: The minimum path sum from top to bottom is 11 (i.e., 2 + 3 + 5 + 1 = 11).
```
Example 2:
```
Input the following triangle:
[
     [2],
    [3,2],
   [6,5,7],
  [4,4,8,1]
]
Output: 12
Explanation: The minimum path sum from top to bottom is 12 (i.e., 2 + 2 + 7 + 1 = 12).
```
Notice: Bonus point if you are able to do this using only O(n) extra space, where n is the total number of rows in the triangle.

# Solution
```python
from functools import lru_cache
class Solution:
    """
    @param triangle: a list of lists of integers
    @return: An integer, minimum path sum
    """   
    def minimumTotal(self, triangle):
        # corner case
        if not triangle:
            return 0
        # pass common data (read only) to workspace
        self.T = triangle
        # find answer in the last row
        i = len(self.T) - 1
        ans = []
        for j in range(len(self.T[i])):
            ans.append(self.dp(i, j))
        # return min of ans
        return min(ans)
    
    @lru_cache(None)
    def dp(self, i, j):
        # if first row, no need to trace back
        if i == 0:
            return self.T[i][j]
        # init for min comparison
        path_sum = float("inf")
        # update answer for left parent path
        if j - 1 >= 0:
            path_sum = min([path_sum, self.T[i][j] + self.dp(i-1, j-1)])
        # update answer for right parent path
        if j < len(self.T[i-1]):
            path_sum = min([path_sum, self.T[i][j] + self.dp(i-1, j)])
        return path_sum
```
另外可以参看[这里](misc/mem_dfs.md)