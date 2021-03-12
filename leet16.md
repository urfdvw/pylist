# [16. 3Sum Closest](https://leetcode.com/problems/3sum-closest/)

Given an array nums of n integers and an integer target, find three integers in nums such that the sum is closest to target. Return the sum of the three integers. You may assume that each input would have exactly one solution.

 

Example 1:

    Input: nums = [-1,2,1,-4], target = 1
    Output: 2
    Explanation: The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).

# Solution
```python
class Solution:
    def threeSumClosest(self, nums: List[int], target: int) -> int:
        nums.sort()
        
        min_diff = float('inf')
        for i in range(len(nums) - 2):
            if i > 0:
                if nums[i] == nums[i-1]:
                    continue
            left = i + 1
            right = len(nums) - 1
            while left < right:
                accu = nums[i] + nums[left] + nums[right]
                diff = abs(accu - target)
                if diff < min_diff:
                    min_diff = diff
                    min_accu = accu
                if accu == target:
                    return target
                elif accu < target:
                    left += 1
                else: # accu > target
                    right -= 1
        return min_accu
```