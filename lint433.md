# [433. Number of Islands](https://lintcode.com/problem/number-of-islands/description?_from=ladder&&fromId=1)
Given a boolean 2D matrix, 0 is represented as the sea, 1 is represented as the island. If two 1 is adjacent, we consider them in the same island. We only consider up/down/left/right adjacent.

Find the number of islands.

Example 1:
```
Input:
[
  [1,1,0,0,0],
  [0,1,0,0,1],
  [0,0,0,1,1],
  [0,0,0,0,0],
  [0,0,0,0,1]
]
Output:
3
```
Example 2:
```
Input:
[
  [1,1]
]
Output:
1
```
## Solutions
```python
class Solution:
    """
    @param grid: a boolean 2D matrix
    @return: an integer
    """
    def numIslands(self, grid):
        # corner case: not even a pixel
        if len(grid) == 0:
            return 0
        if len(grid[0]) == 0:
            return 0
        #
        n_island = 0
        queued = set()
        # loop of all possible pixel
        for i in range(len(grid)):
            for j in range(len(grid[0])):
                if grid[i][j] == 0: # if pixel not land
                    continue
                if (i, j) in queued: # if ever visited
                    continue
                # new island found
                n_island += 1
                # visit all pixel of the island by BFS
                queue = collections.deque([(i, j)])
                queued.add((i, j))
                while queue:
                    # current pixel position
                    c_i, c_j = queue.popleft()
                    neighbors = self.find_neighbors(grid, c_i, c_j)
                    for nei in neighbors:
                        if nei not in queued:
                            queue.append(nei)
                            queued.add(nei)
        return n_island
        
    def is_land(self, grid, i, j):
        """ find if (i, j) is a pixel representing land
        in:
            grid: list of list of bool
            i,j: int: co-ordinate
        out:
            bool: true if pixel (i, j) is a land pixel
        """
        if i < 0 or i >= len(grid):
            return False
        if j < 0 or j >= len(grid[0]):
            return False
        if grid[i][j] == 0:
            return False
        return True
            
    def find_neighbors(self, grid, i, j):
        """ find possible neighbors according to just grid
        in:
            grid: list of list of bool
            i,j: int: co-ordinate
        out:
            list of tuple: co-ordinate of neighbors
        """
        alter = [(0, 1), (1, 0), (0, -1), (-1, 0)]
        neighbors = []
        for a in alter:
            x, y = (i + a[0], j + a[1])
            if self.is_land(grid, x, y):
                neighbors.append((x,y))
        return neighbors
```

Special care:
- avoid using try catch
- ```(1, 2) + (3, 4)``` returns ```(4, 6)```, so `alter` need to be breaked in to 2 parts
- check ```len(grid)``` then ```len(grid[0])```, don't forget ```[0]```
- 地图搜索题一般都有一个**边界函数**和一个**邻居寻找函数**
- 因为BSF退出时候`queued`会保存所有访问过的地点，所以在位置循环里面，可以用`queued`作为是否访问过的标记。