# [64. Minimum Path Sum](https://leetcode.com/problems/minimum-path-sum/)

Given a m x n grid filled with non-negative numbers, find a path from top left to bottom right which minimizes the sum of all numbers along its path.

Note: You can only move either down or right at any point in time.

Example:

    Input:
    [
    [1,3,1],
    [1,5,1],
    [4,2,1]
    ]
    Output: 7
    Explanation: Because the path 1→3→1→1→1 minimizes the sum.

# Solution
```python
from functools import lru_cache
class Solution:
    def minPathSum(self, grid: List[List[int]]) -> int:
        if len(grid) == 0 or len(grid[0]) == 0:
            return 0
        self.grid = grid
        return self.dc(len(grid)-1, len(grid[0])-1)
    
    @lru_cache(None)
    def dc(self, i, j):
        if i == 0 and j == 0:
            return self.grid[i][j]
        
        if i == 0:
            return self.dc(i, j-1) + self.grid[i][j]
        
        if j == 0:
            return self.dc(i-1, j) + self.grid[i][j]
        
        return min(self.dc(i, j-1), self.dc(i-1, j)) + self.grid[i][j]
```

# Care
- `functools` 库名称是有复数的