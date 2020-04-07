# [110. Minimum Path Sum](https://www.lintcode.com/problem/minimum-path-sum/description)
Given a m x n grid filled with non-negative numbers, find a path from top left to bottom right which minimizes the sum of all numbers along its path.

Example 1:

	Input:  [[1,3,1],[1,5,1],[4,2,1]]
	Output: 7
	
	Explanation:
	Path is: 1 -> 3 -> 1 -> 1 -> 1


Example 2:

	Input:  [[1,3,2]]
	Output: 6
	
	Explanation:  
	Path is: 1 -> 3 -> 2

Notice

    You can only go right or down in the path

# solution
```python
from functools import lru_cache
class Solution:
    """
    @param grid: a list of lists of integers
    @return: An integer, minimizes the sum of all numbers along its path
    """
    def minPathSum(self, grid):
        self.grid = grid
        return self.dp(len(grid)-1, len(grid[0])-1)
        
    
    @lru_cache(None)
    def dp(self, m, n):
        if m < 0 or n < 0:
            return float('inf')
        if m == 0 and n == 0:
            return self.grid[0][0]
        return min([self.dp(m-1, n), self.dp(m, n-1)]) + self.grid[m][n]
            
# care  float('inf'), and 0,0
```

# Care
- `float('inf') `是为了在求最小时候让越界的坐标返回无用的值
- 然而（0，0）这个坐标两边都是越界，要单独定义