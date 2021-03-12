# [18. 4Sum](https://leetcode.com/problems/4sum/)

Given an array nums of n integers and an integer target, are there elements a, b, c, and d in nums such that a + b + c + d = target? Find all unique quadruplets in the array which gives the sum of target.

Notice that the solution set must not contain duplicate quadruplets.

 

Example 1:

    Input: nums = [1,0,-1,0,-2,2], target = 0
    Output: [[-2,-1,1,2],[-2,0,0,2],[-1,0,0,1]]

Example 2:

    Input: nums = [], target = 0
    Output: []

# Solution
```python
class Solution:
    def fourSum(self, nums: List[int], target: int) -> List[List[int]]:
        nums.sort()
        
        ans = list()
        for i in range(len(nums) - 3):
            if i > 0:
                if nums[i] == nums[i-1]:
                    continue
            for j in range(i+1, len(nums) - 2):
                if j > i+1:
                    if nums[j] == nums[j-1]:
                        continue
                left = j + 1
                right = len(nums) - 1
                while left < right:
                    accu = nums[i] + nums[j] + nums[left] + nums[right]
                    if accu == target:
                        ans.append([nums[i], nums[j], nums[left], nums[right]])
                        right -= 1
                        left += 1
                        while left < right and nums[left] == nums[left-1]:
                            left += 1
                    elif accu < target:
                        left += 1
                    else:
                        right -= 1
        return ans
```

## Ksum
```python
class Solution:
    def fourSum(self, nums: List[int], target: int) -> List[List[int]]:
        nums.sort()
        return self.kSum(nums, target, 4)
        
    def kSum(self, nums, target, k):
        if k == 2:
            return self.twoSum(nums, target)
        
        ans = list()
        for i in range(len(nums) - (k-1)):
            if i > 0:
                if nums[i] == nums[i-1]:
                    continue
            ans += [[nums[i]] + a for a in self.kSum(nums[i+1:], target-nums[i], k-1)]
        return ans
    
    def twoSum(self, nums, target):
        ans = []
        left = 0
        right = len(nums) - 1
        while left < right:
            accu = nums[left] + nums[right]
            if accu == target:
                ans.append([nums[left], nums[right]])
                right -= 1
                left += 1
                while left < right and nums[left] == nums[left-1]:
                    left += 1
            elif accu < target:
                left += 1
            else:
                right -= 1
        return ans
```