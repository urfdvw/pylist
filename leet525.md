# [525. Contiguous Array](https://leetcode.com/problems/contiguous-array/)

Given a binary array, find the maximum length of a contiguous subarray with equal number of 0 and 1.

Example 1:

    Input: [0,1]
    Output: 2
    Explanation: [0, 1] is the longest contiguous subarray with equal number of 0 and 1.
Example 2:

    Input: [0,1,0]
    Output: 2
    Explanation: [0, 1] (or [1, 0]) is a longest contiguous subarray with equal number of 0 and 1.
Note: The length of the given binary array will not exceed 50,000.

# Solution
```python
class Solution:
    def findMaxLength(self, nums: List[int]) -> int:
        d = dict() # key: accumulated sum, value: index
        d[0] = -1
        accu = 0
        for i, n in enumerate(nums):
            if n == 1:
                accu += 1
            else:
                accu -= 1
            if accu not in d:
                d[accu] = i
            # if accu in d: # not necessary
            #     d[accu] = min(d[accu], i)
            
        accu = 0
        max_len = 0
        for i, n in enumerate(nums):
            if n == 1:
                accu += 1
            else:
                accu -= 1
            max_len = max(max_len, i - d[accu])
            
        return max_len
```
# Care
- 注意 max 和 min 擂台的初始化
    - 根据题目要求，不一定要初始化到正负无穷
    - 比如这里 max 初始化到 0 就可以