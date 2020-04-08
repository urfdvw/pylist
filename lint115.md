# [115. Unique Paths II](https://www.lintcode.com/problem/unique-paths-ii/description)

Follow up for "Unique Paths":

Now consider if some obstacles are added to the grids. How many unique paths would there be?

An obstacle and empty space is marked as 1 and 0 respectively in the grid.

Example 1:

    Input: [[0]]
    Output: 1


Example 2:

    Input:  [[0,0,0],[0,1,0],[0,0,0]]
    Output: 2
    
    Explanation:
    Only 2 different path.
	

Notice

    m and n will be at most 100.
    

# Solution
```python
from functools import lru_cache
class Solution:
    """
    @param obstacleGrid: A list of lists of integers
    @return: An integer
    """
    def uniquePathsWithObstacles(self, obstacleGrid):
        self.grid = obstacleGrid
        return self.dp(len(obstacleGrid)-1, len(obstacleGrid[0])-1)
        
    
    @lru_cache(None)
    def dp(self, m, n):
        if self.grid[m][n] == 1:
            return 0
        if m == 0 and n == 0:
            return 1
        if m < 0 or n < 0:
            return 0
        return self.dp(m-1, n) + self.dp(m, n-1)
```
# care
- this cannot be true any more: 
    - if m == 0 or n == 0:
        - return 1