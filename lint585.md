# [585. Maximum Number in Mountain Sequence](https://www.lintcode.com/problem/maximum-number-in-mountain-sequence/description)

Given a mountain sequence of n integers which increase firstly and then decrease, find the mountain top.

Example 1:
```
Input: nums = [1, 2, 4, 8, 6, 3] 
Output: 8
```
Example 2:
```
Input: nums = [10, 9, 8, 7], 
Output: 10
```

## Solution
```python
class Solution:
    """
    @param nums: a mountain sequence which increase firstly and then decrease
    @return: then mountain top
    """
    def mountainSequence(self, nums):
        # less than 2 elements
        if len(nums) == 0:
            # no such case
            return "nimei"
        if len(nums) <= 2:
            return max(nums)
        # corner cases: not increase or decrease at all
        if nums[0] > nums[1]:
            return nums[0]
        if nums[-1] > nums[-2]:
            return nums[-1]
        # init
        low = 0
        up = len(nums) - 1
        # binary search loop
        while low < up - 1:
            mid = (low + up) // 2
            if nums[mid] < nums[mid + 1]:
                low = mid
            if nums[mid] > nums[mid + 1]:
                up = mid
            if nums[mid] == nums[mid + 1]:
                # no such case
                return "nimei"
        # definitly up
        return nums[up]
```
question
- What is the minimum possible length of the sequence? At least 1!
- Can I assume that increase or decrease means "strictly" increasing and decreasing? Yes!

special care
- there is a F test case did not increase or decrease at all
- BS by condition, because the answers are divided into increasing half and decreasing half