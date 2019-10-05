# [611. Knight Shortest Path](https://www.lintcode.com/problem/knight-shortest-path/description)

Given a knight in a chessboard (a binary matrix with 0 as empty and 1 as barrier) with a source position, find the shortest path to a destination position, return the length of the route.
Return -1 if destination cannot be reached.

- source and destination must be empty. (one corner case is not necessary)
- Knight can not enter the barrier.
- Path length refers to the number of steps the knight takes.

If the knight is at (x, y), he can get to the following positions in one step:
```
(x + 1, y + 2)
(x + 1, y - 2)
(x - 1, y + 2)
(x - 1, y - 2)
(x + 2, y + 1)
(x + 2, y - 1)
(x - 2, y + 1)
(x - 2, y - 1)
```
Example 1:
```
Input:
[[0,0,0],
 [0,0,0],
 [0,0,0]]
source = [2, 0] destination = [2, 2] 
Output: 2
Explanation:
[2,0]->[0,1]->[2,2]
```
Example 2:
```
Input:
[[0,1,0],
 [0,0,1],
 [0,0,0]]
source = [2, 0] destination = [2, 2] 
Output:-1
```
## Solution
```python
"""
Definition for a point.
class Point:
    def __init__(self, a=0, b=0):
        self.x = a
        self.y = b
"""
import collections
class Solution:
    """
    @param grid: a chessboard included 0 (false) and 1 (true)
    @param source: a point
    @param destination: a point
    @return: the shortest path 
    """
    def shortestPath(self, grid, source, destination):
        # corner case
        ## empty set insane
        if len(grid) == 0:
            return -1
        if len(grid[0]) == 0:
            return -1
        ## start or end has barrier
        if not self.can_move_to(grid, source.x, source.y):
            return -1
        if not self.can_move_to(grid, destination.x, destination.y):
            return -1
            
        # BFS serch for destination
        queue = collections.deque([(source.x, source.y)])
        queued = set(queue)
        n_steps = 0 # counter of steps: layer in BFS
        while queue:
            for _ in range(len(queue)):
                x, y = queue.popleft()
                if x == destination.x and y == destination.y:
                    return n_steps
                neis = self.positions_next_step(grid, x, y)
                for nei in neis:
                    if nei not in queued:
                        queue.append(nei)
                        queued.add(nei)
            n_steps += 1
        return -1
        
    def can_move_to(self, grid, x, y):
        """
        in:
            grid: list of list: len(grid) > 0
            x,y: int: position to check
        out:
            bool: true when (x, y) is a valid position
        """
        if x < 0 or x >= len(grid):
            return False
        if y < 0 or y >= len(grid[0]):
            return False
        if grid[x][y] != 0:
            return False
        return True
        
    def positions_next_step(self, grid, x, y):
        """
        in:
            grid: list of list: len(grid) > 0
            x,y: int: position to check
        out:
            list of tuple of int: position of possible neighbors
        """
        alter = [(1, 2),
                 (1, -2),
                 (-1, 2),
                 (-1, -2),
                 (2, 1),
                 (2, -1),
                 (-2, 1),
                 (-2, -1),
                 ]
        neighbors = []
        for a in alter:
            x_n, y_n = x + a[0], y + a[1]
            if self.can_move_to(grid, x_n, y_n):
                neighbors.append((x_n, y_n))
        return neighbors
```
Special care:
- 這是一個很明顯的隱式圖不能add對象to qeueued的例子，better way is just work with tuple with out touching the objects.