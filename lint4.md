# [4. Ugly Number II](https://www.lintcode.com/problem/ugly-number-ii/description)

Ugly number is a number that only have prime factors 2, 3 and 5.

Design an algorithm to find the nth ugly number. The first 10 ugly numbers are 1, 2, 3, 4, 5, 6, 8, 9, 10, 12...

Example 1:
```
Input: 9
Output: 10
```
Example 2:
```
Input: 1
Output: 1
Challenge
O(n log n) or O(n) time.
```
Notice: Note that 1 is typically treated as an ugly number.

# Binary search Solution
O(nlogn) 的复杂度
```python
class Solution:
    """
    @param n: An integer
    @return: return a  integer as description.
    """
    def nthUglyNumber(self, n):
        nums = [1, 2, 3, 4, 5]
        if n <= len(nums):
            return nums[n-1]
            
        while len(nums) < n:
            candi = []
            for f in [2, 3, 5]:
                up = len(nums)-1
                low = 0
                # bi-search to find the lowest i that
                # nums[i] * f > num[-1]
                while up - low > 1:
                    mid = low + (up - low) // 2
                    # if condition satisfied
                    if nums[mid] * f > nums[-1]:
                        up = mid
                    else:
                        low = mid
                candi.append(nums[up] * f)
            nums.append(min(candi))
            
        return nums[-1]
```
- 思路就是，用二分法分别找到用*2， *3， *5能做出来的，最小的，大于目前最大数的数字。
- 需要注意的点是corner case。因为二分法必须从“前端不满足，后端满足”的数据上做。然而开始的数组太小，比如[1， 2]前后端都满足条件（1 * 3>2, 2 * 3>2）所以只能从比较大的数组开始。其中最小的最后一个数必须>=5。

# Heap solution
```python
from heapq import heappush, heappop
class Solution:
    """
    @param n: An integer
    @return: return a  integer as description.
    """
    def nthUglyNumber(self, n):
        if n == 1:
            return 1
            
        nums = [1]
        h = []
        pushed = set()
        while len(nums) < n:
            for f in [2, 3, 5]:
                candi = nums[-1] * f
                if candi not in pushed:
                    heappush(h, candi)
                    pushed.add(candi)
            nums.append(heappop(h))
        return nums[-1]            
```
