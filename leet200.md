# [200. Number of Islands](https://leetcode.com/problems/number-of-islands/)

Given a 2d grid map of '1's (land) and '0's (water), count the number of islands. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

Example 1:

    Input:
    11110
    11010
    11000
    00000

    Output: 1
Example 2:

    Input:
    11000
    11000
    00100
    00011

    Output: 3

# Solution
```python
from collections import deque
class Solution:
    def numIslands(self, grid: List[List[str]]) -> int:
        if len(grid) == 0 or len(grid[0]) == 0 :
            return 0
        
        count = 0
        visited = set()
        for i in range(len(grid)):
            for j in range(len(grid[0])):
                if grid[i][j] == '0' or (i, j) in visited:
                    continue
                    
                count += 1 # number of bfs iteration(s)
                q = deque([(i, j)])
                while len(q) > 0:
                    node = q.popleft()
                    neighbors = self.find_neighbors(node, grid)
                    for nei in neighbors:
                        if grid[nei[0]][nei[1]] == '1' and nei not in visited:
                            q.append(nei)
                            visited.add(nei)
        return count
    
    def find_neighbors(self, node, grid):
        neighbors = []
        alter = [(0, 1), (1, 0), (0, -1), (-1, 0)]
        for a in alter:
            x = node[0] + a[0]
            y = node[1] + a[1]
            if self.in_grid((x, y), grid):
                neighbors.append((x, y))
        return neighbors
    
    def in_grid(self, node, grid):
        if node[0] < 0 or node[0] >= len(grid):
            return False
        if node[1] < 0 or node[1] >= len(grid[0]):
            return False
        return True
```
# Care
- 犯的常规错误
    - deque()初始化的时候，里面一定要放一个list。
        - 特别是每个元素都是tuple的时候，要放一个list of tuple
    - `True`大写
    - list of list 的双下标应该是 `[i][j]` 因为不是 numpy
    - 判断要不要放 q 里的时候，一定先看一下 qed 里面是不是已经有了。q 和 qed 一定共同进退
    - 一个输入参数一定看好格式，0 和 1 有可能是字符。