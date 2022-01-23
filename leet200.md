# [200. Number of Islands](https://leetcode.com/problems/number-of-islands/)

Given a 2d grid map of '1's (land) and '0's (water), count the number of islands. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

Example 1:

    Input: grid = [
    ["1","1","1","1","0"],
    ["1","1","0","1","0"],
    ["1","1","0","0","0"],
    ["0","0","0","0","0"]
    ]
    Output: 1

Example 2:

    Input: grid = [
    ["1","1","0","0","0"],
    ["1","1","0","0","0"],
    ["0","0","1","0","0"],
    ["0","0","0","1","1"]
    ]
    Output: 3

Constraints:
- m == grid.length
- n == grid[i].length
- 1 <= m, n <= 300
- grid[i][j] is '0' or '1'.

# Solution
```python
class Solution:
    def numIslands(self, grid: List[List[str]]) -> int:
        counter = 0 # counter for inslands
        qed = set() # record ever enqueued locations
        # loop iterate thorouh all locations
        for i in range(len(grid)):
            for j in range(len(grid[0])):
                # if it is a new island
                if (grid[i][j] == '1' # if island
                    and (i, j) not in qed): # if never entered the queue
                    counter += 1 # add one island
                    # bsf traverse to visit all locations of the current island
                    q = deque([(i, j)]) # queue for a single island
                    while q: # if queue not empty
                        node = q.popleft() # current location
                        neis = self.get_neis(grid, node) # get all neighbors
                        for n in neis: # iterate through
                            if n not in qed: # if never enqueued
                                q.append(n) # enqueue
                                qed.add(n) # record enqueue
        return counter
    
    def get_neis(self, grid, node):
        alter = [
            (1, 0),
            (0, 1),
            (-1, 0),
            (0, -1),
        ] # 4 directions
        out = [
            tuple(a[i] + node[i] for i in range(2)) # two axes
            for a in alter 
        ] # 4 directions from the node
        out = [
            n for n in out
            if 0 <= n[0] < len(grid) 
            and 0 <= n[1] < len(grid[0]) # if in the grid
            and grid[n[0]][n[1]] == '1' # if is island
        ] # all possible neighbors
        return out
```
```steps
1, 2
```
[Code Steps](./presentations/?id=leet200)

思路
- 能把两个坐标一起处理的时候尽量一起处理，两个坐标绑在一个 tuple 里方便 set 查重。

Python 要点
- ```tuple``` comprehension 的写法是 ```tupple( ... )``` 而不是 ```()```
    - ref: https://stackoverflow.com/a/16940351/7037749
- double list comprehension  的顺序是 和 嵌套 for 的顺讯是一样的
    - ref：https://stackoverflow.com/a/36734643/7037749
- ```()``` 内可以在运算符之前或者之后换行。
    - 所以，如果遇到 if 有多个条件的时候，可以用 ```if ():``` 然后括号里有多行
    - Comprehension 以为也带着括号，所以可以在关键词处换行
- Python 里面的判断大小的 ```<```,```<=``` 等符号可以串联，以省略一堆 ```and```

# Arcived Solution
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