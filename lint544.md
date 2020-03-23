# [544. Top k Largest Numbers](https://www.lintcode.com/problem/top-k-largest-numbers/description)
Given an integer array, find the top k largest numbers in it.

Example
```
Example1

Input: [3, 10, 1000, -99, 4, 100] and k = 3
Output: [1000, 100, 10]

Example2
Input: [8, 7, 6, 5, 4, 3, 2, 1] and k = 5
Output: [8, 7, 6, 5, 4]
```
# solution
```python
from heapq import heappush, heappop
class Solution:
    """
    @param nums: an integer array
    @param k: An integer
    @return: the top k largest numbers in array
    """
    def topk(self, nums, k):
        h = []
        for n in nums:
            if len(h) < k:
                heappush(h, n)
                continue
            
            if n > h[0]:
                heappop(h)
                heappush(h, n)
        ans = []
        while len(h) > 0:
            ans.append(heappop(h))
        return ans[::-1]
```