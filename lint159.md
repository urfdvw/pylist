# [159. Find Minimum in Rotated Sorted Array](https://www.lintcode.com/problem/find-minimum-in-rotated-sorted-array/description)

Suppose a sorted array is rotated at some pivot unknown to you beforehand.

(i.e., 0 1 2 4 5 6 7 might become 4 5 6 7 0 1 2).

Find the minimum element.

Example 1:
```
Input：[4, 5, 6, 7, 0, 1, 2]
Output：0
Explanation：
The minimum value in an array is 0.
```
Example 2:
```
Input：[2,1]
Output：1
Explanation：
The minimum value in an array is 1.
```

## Solution:
```python
class Solution:
    """
    @param nums: a rotated sorted array
    @return: the minimum number in the array
    """
    def findMin(self, nums):
        # corner cases
        ## only one element:
        if len(nums) == 1:
            return nums[0]
        ## not rotated at all
        if nums[0] < nums[-1]:
            return nums[0]
        
        # --- binary search by condition ---
        # find the first element that smaller than nums[0]
        
        # init
        up = len(nums)  # should satisfy
        low = 0  # should not satisfy
        while low + 1 < up:
            mid = int((up - low)/2 + low)
            if nums[mid] < nums[0]:
                up = mid
            else:
                low = mid
        # return up or low
        ## first after the boundary
        return nums[up]  # return the element, not the index
```
questions:
- Q: what if all same numbers such as [1, 1, 1, 1, 1]?
    - A: no duplicated so no such case.
- Q: what to return if empty array?
    - A: no such case
        
special care
- return the element not the index