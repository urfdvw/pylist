# [1. Two Sum](https://leetcode.com/problems/two-sum/)

Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

You can return the answer in any order.

 

Example 1:

    Input: nums = [2,7,11,15], target = 9
    Output: [0,1]
    Output: Because nums[0] + nums[1] == 9, we return [0, 1].

Example 2:

    Input: nums = [3,2,4], target = 6
    Output: [1,2]

Example 3:

    Input: nums = [3,3], target = 6
    Output: [0,1]

# Solution
```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        nums = list(zip(nums, [i for i in range(len(nums))]))
        nums.sort()
        left = 0
        right = len(nums) - 1
        while left < right:
            if nums[left][0] + nums[right][0] == target:
                return [nums[left][1], nums[right][1]]
            if nums[left][0] + nums[right][0] < target:
                left += 1
                continue
            if nums[left][0] + nums[right][0] > target:
                right -= 1
```