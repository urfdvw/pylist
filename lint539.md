# [539. Move Zeroes](https://www.lintcode.com/problem/move-zeroes/description)
Given an array nums, write a function to move all 0's to the end of it while maintaining the relative order of the non-zero elements.

You must do this in-place without making a copy of the array.
Minimize the total number of operations.

Example 1:
```
Input: nums = [0, 1, 0, 3, 12],
Output: [1, 3, 12, 0, 0].
```
Example 2:
```
Input: nums = [0, 0, 0, 3, 1],
Output: [3, 1, 0, 0, 0].
```
# solution
```python
class Solution:
    """
    @param nums: an integer array
    @return: nothing
    """
    def moveZeroes(self, nums):
        write = 0
        for read in range(len(nums)):
            if nums[read] != 0:
                nums[write] = nums[read]
                write += 1
        while write < len(nums):
            nums[write] = 0
            write += 1
        return nums
```
# special care
- `write`表示下一个准备被写入的位置
- `read`因为只要一遍，所以可以直接用forloop