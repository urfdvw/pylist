# [33. Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/)

Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.

(i.e., [0,1,2,4,5,6,7] might become [4,5,6,7,0,1,2]).

You are given a target value to search. If found in the array return its index, otherwise return -1.

You may assume no duplicate exists in the array.

Your algorithm's runtime complexity must be in the order of O(log n).

Example 1:

    Input: nums = [4,5,6,7,0,1,2], target = 0
    Output: 4
Example 2:

    Input: nums = [4,5,6,7,0,1,2], target = 3
    Output: -1

# Solution
```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        if len(nums) == 0:
            return -1
        if len(nums) == 1:
            if nums[0] == target:
                return 0
            else:
                return -1
            
        low = 0
        up = len(nums) - 1
        while up - low > 1:
            mid = low + (up - low) // 2
            if nums[mid] == target:
                return mid
            if nums[mid] > nums[low]: # first half is not rotated
                if target >= nums[low] and target < nums[mid]: # target in this first half
                    up = mid
                else:
                    low = mid
            else: # 2nd half is not rotated
                if target > nums[mid] and target <= nums[up]: # target in this 2nd half
                    low = mid
                else:
                    up = mid
                    
        if nums[up] == target:
            return up
        if nums[low] == target:
            return low
        return -1
```

# care
- 二分法不是想当然的不是up就是low，还有找不到的时候
    - 最后返回的时候要判断两次，return 3 次
- copy 的代码，一定要好像重新写一样，完整得读一遍，边读边改。因为很多细节都不一样，有可能会遗漏。