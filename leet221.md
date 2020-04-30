# [221. Maximal Square](https://leetcode.com/problems/maximal-square/)

Given a 2D binary matrix filled with 0's and 1's, find the largest square containing only 1's and return its area.

Example:

    Input: 

    1 0 1 0 0
    1 0 1 1 1
    1 1 1 1 1
    1 0 0 1 0

    Output: 4

# Solution
```python
from functools import lru_cache
class Solution:
    def maximalSquare(self, matrix: List[List[str]]) -> int:
        if len(matrix) == 0 or len(matrix[0]) == 0:
            return 0

        for i in range(len(matrix)):
            for j in range(len(matrix[0])):
                matrix[i][j] = int(matrix[i][j])
                
        left = [a + [] for a in matrix] + []
        up = [a + [] for a in matrix] + []
        
        for i in range(len(left)):
            for j in range(1, len(left[0])):
                left[i][j] *= left[i][j] + left[i][j-1]
        for j in range(len(up[0])):
            for i in range(1, len(up)):
                up[i][j] *= up[i][j] + up[i-1][j]
                
        self.left = left
        self.up = up
        self.mat = matrix
        max_size = 0
        
        out = [a + [] for a in matrix] + []
        for i in range(len(matrix)):
            for j in range(len(matrix[0])):
                size = self.dc(i, j)
                out[i][j] = size
                # record max
                max_size = max(max_size, size)
        print(out)
        print(up)
        return max_size * max_size
        
    
    @lru_cache(None)
    def dc(self, i, j):
        if self.mat[i][j] == 0:
            return 0
        
        if i == 0 or j == 0:
            return 1
        
        # general logic
        size = min([self.left[i][j], self.up[i][j], self.dc(i-1, j-1)+1])
        
        return size
```

# Care
- 尼玛看题，看题，看题。第一次看成求和，第二次看成长方形我真是服了。
- list of list deep copy:
    - `left = [a + [] for a in matrix] + []`
- 这题有 insane empty test case