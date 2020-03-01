# 记忆化搜索

这里用的例子是[109. Triangle](https://www.lintcode.com/problem/triangle/description)

一个标准的DFS答案是这么写的：
```python
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
当然是妥妥的TLE

于是我们可以用一个Dict保存答案，如果算过就直接调答案，如果没算过再算。

```python
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
        
    def __init__(self):
        self.dp_data = dict()
        
    def dp_fun(self, i, j):
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
        
    def dp(self, i, j):
        """
        path sum to T[i][j]
        """
        if (i, j) not in self.dp_data:
            self.dp_data[(i, j)] = self.dp_fun(i, j)
        return self.dp_data[(i, j)]
```

另外还有一个decorator叫lru_cache实现了完全相同的功能。只不过它用的不是dict而是ordered dict。

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

就是记得先import。