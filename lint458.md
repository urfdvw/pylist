# [458. Last Position of Target](https://www.lintcode.com/problem/last-position-of-target/description)
Find the ***last*** position of a target number in a sorted array. Return -1 if target does not exist.

Example 1:
```
Input: nums = [1,2,2,4,5,5], target = 2
Output: 2
```
Example 2:
```
Input: nums = [1,2,2,4,5,5], target = 6
Output: -1
```

## Solution
```python
class Solution:
    """
    @param nums: An integer array sorted in ascending order
    @param target: An integer
    @return: An integer
    """
    def lastPosition(self, nums, target):
        # corner cases
        if not nums:
            return -1
        # init boundaries
        up = len(nums) - 1 
        low = 0
        # while up and low are not next to each other
        while up > low + 1:
            mid = int(low + (up - low)/2)
            if nums[mid] == target:
                # because 'last', mid can be larger
                low = mid
            elif nums[mid] > target:
                up = mid
            else:  # (nums[mid] < target)
                low = mid
        # check wether up or low
        # because 'last', check the larger one first
        if nums[up] == target:
            return up
        if nums[low] == target:
            return low
        # if not found
        return -1
```
[Binary search notes](readme.md#Binary-search)