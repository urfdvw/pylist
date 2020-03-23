# [612. K Closest Points](https://www.lintcode.com/problem/k-closest-points/description)

Given some points and an origin point in two-dimensional space, find k points which are nearest to the origin.
Return these points sorted by distance, if they are same in distance, sorted by the x-axis, and if they are same in the x-axis, sorted by y-axis.

Example 1:
```
Input: points = [[4,6],[4,7],[4,4],[2,5],[1,1]], origin = [0, 0], k = 3 
Output: [[1,1],[2,5],[4,4]]
```
Example 2:
```
Input: points = [[0,0],[0,9]], origin = [3, 1], k = 1
Output: [[0,0]]
```
# Solution
```python
"""
Definition for a point.
class Point:
    def __init__(self, a=0, b=0):
        self.x = a
        self.y = b
"""
from heapq import heappush, heappop
class Solution:
    """
    @param points: a list of points
    @param origin: a point
    @param k: An integer
    @return: the k closest points
    """
    def kClosest(self, points, origin, k):
        h = []
        for i, p in enumerate(points):
            d = self.dist(origin, p)
            if len(h) < k:
                heappush(h, [-d, -p.x, -p.y, i, p])
                continue
            flag = False
            if [-d, -p.x, -p.y] > h[0][0:3]:
                heappop(h)
                heappush(h, [-d, -p.x, -p.y, i, p])
        ans = []
        for _ in range(len(h)):
            ans.append(heappop(h)[4])
        return ans[::-1]
    
    def dist(self, p1, p2):
        dx = p1.x - p2.x
        dy = p1.y - p2.y
        return dx * dx + dy * dy
```
# care
- 这个题的最烦的点就是
    - 同距离的点排序
    - 同一个点排序
- 同距离的点要按照先x后y的顺序排序
    - 首先要在heap里面排序
        - 所以要在每个sublist里面先按顺序写入d，x，y。
        - 而且是负的因为是maxheap
    - 而且在比较heaptop和新点的时候也要考虑。
        - 距离相等的话比较 x
        - x相等的话比较 y
        - 这个正好是list的功能。可以用
            ```python
            if [-d, -p.x, -p.y] > h[0][0:3]:
            ```
            替代
            ```python
            if -d > h[0][0]:
                flag = True
            if -d == h[0][0] and -p.x > h[0][1]:
                flag = True
            if -d == h[0][0] and -p.x == h[0][1] and -p.y > h[0][2]:
                flag = True
            if flag:
            ```
            （终于优雅了一些）
- 如果是完全相同的点的话，在heap比较的时候，无法比较挂在最后的点那个point object。
    - 为了避免这个情况，要在object前面挂一个每个点都不同的数字，这样可以阻断比较的过程
        - 可以挂一个随机数
        - 不过这里有循环的index我们就挂一个index
