# [53. Maximum Subarray](https://leetcode.com/problems/maximum-subarray/)

Given an integer array nums, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

Example:

    Input: [-2,1,-3,4,-1,2,1,-5,4],
    Output: 6
    Explanation: [4,-1,2,1] has the largest sum = 6.
Follow up:

    If you have figured out the O(n) solution, try coding another solution using the divide and conquer approach, which is more subtle.
# Solutions
```python
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        max_sum = -float('inf')
        min_sum = 0
        cum = 0
        for n in nums:
            cum += n
            max_sum = max(max_sum, cum - min_sum)
            min_sum = min(min_sum, cum)
            
        return max_sum
```