# [283. Move Zeroes](https://leetcode.com/problems/move-zeroes/)

Given an array nums, write a function to move all 0's to the end of it while maintaining the relative order of the non-zero elements.

Example:

    Input: [0,1,0,3,12]
    Output: [1,3,12,0,0]
Note:

    You must do this in-place without making a copy of the array.
    Minimize the total number of operations.

# Solution
```python
class Solution:
    def moveZeroes(self, nums: List[int]) -> None:
        if len(nums) < 2:
            return nums
        write = 0
        for read in range(len(nums)):
            if nums[read] == 0 :
                continue
            nums[write] = nums[read]
            write += 1
            
        while write < len(nums):
            nums[write] = 0
            write += 1
```