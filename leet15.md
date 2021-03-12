# [15. 3Sum](https://leetcode.com/problems/3sum/)

Given an array nums of n integers, are there elements a, b, c in nums such that a + b + c = 0? Find all unique triplets in the array which gives the sum of zero.

Notice that the solution set must not contain duplicate triplets.

 

Example 1:

    Input: nums = [-1,0,1,2,-1,-4]
    Output: [[-1,-1,2],[-1,0,1]]

Example 2:

    Input: nums = []
    Output: []

Example 3:

    Input: nums = [0]
    Output: []

# Solution
```python
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        nums.sort()
        
        ans = list()
        for i in range(len(nums) - 2):
            if i > 0:
                if nums[i] == nums[i-1]:
                    continue
            left = i + 1
            right = len(nums) - 1
            while left < right:
                accu = nums[i] + nums[left] + nums[right]
                if accu == 0:
                    ans.append([nums[i], nums[left], nums[right]])
                    right -= 1
                    left += 1
                    while left < right and nums[left] == nums[left-1]:
                        left += 1
                elif accu < 0:
                    left += 1
                else: # accu > 0
                    right -= 1
        return ans
```