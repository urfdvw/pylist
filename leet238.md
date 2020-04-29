# [238. Product of Array Except Self](https://leetcode.com/problems/product-of-array-except-self/)

Given an array nums of n integers where n > 1,  return an array output such that output[i] is equal to the product of all the elements of nums except nums[i].

Example:

    Input:  [1,2,3,4]
    Output: [24,12,8,6]
    Constraint: It's guaranteed that the product of the elements of any prefix or suffix of the array (including the whole array) fits in a 32 bit integer.

Note: Please solve it without division and in O(n).

Follow up:

    Could you solve it with constant space complexity? (The output array does not count as extra space for the purpose of space complexity analysis.)

# Solution

initial solution (more clear, but not constant space)

```python
class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:
        l2r = [1 for i in range(len(nums))]
        r2l = [1 for i in range(len(nums))]
        
        prod = nums[0]
        for i in range(1, len(nums)):
            l2r[i] = prod
            prod *= nums[i]
        
        prod = nums[-1]
        for i in range(len(nums)-2, -1, -1):
            r2l[i] = prod
            prod *= nums[i]
            
        return [l2r[i] * r2l[i] for i in range(len(nums))]
```

The 2 arrays does not have overlap, so that can be combined

```python
class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:
        ans = [1 for i in range(len(nums))]
        
        prod = nums[0]
        for i in range(1, len(nums)):
            ans[i] *= prod
            prod *= nums[i]
        
        prod = nums[-1]
        for i in range(len(nums)-2, -1, -1):
            ans[i] *= prod
            prod *= nums[i]
            
        return ans
```