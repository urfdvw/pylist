# [560. Subarray Sum Equals K](https://leetcode.com/problems/subarray-sum-equals-k/)

Given an array of integers and an integer k, you need to find the total number of continuous subarrays whose sum equals to k.

Example 1:

    Input:nums = [1,1,1], k = 2
    Output: 2

Note:
- The length of the array is in range [1, 20,000].
- The range of numbers in the array is [-1000, 1000] and the range of the integer k is [-1e7, 1e7].

# Solution
Refined submission, use counter
```python
class Solution:
    def subarraySum(self, nums: List[int], k: int) -> int:
        counter = 0
        inv_cum = InvCumsum()
        for i in range(len(nums)):
            # k itself is a satisfied subarray
            if k == nums[i]:
                counter += 1
            # k and previous elements can construct satisfied subarrays
            counter += inv_cum.n_indexes(k - nums[i])
            # update
            inv_cum.append(nums[i])
        return counter
    
class InvCumsum:
    def __init__(self):
        self.sum_of_all = 0
        self.cumsum = dict() # without current element
        
    def append(self, x):
        self.cumsum.setdefault(self.sum_of_all, 0)
        self.cumsum[self.sum_of_all] += 1
        self.sum_of_all += x
        
    def n_indexes(self, inv_cum):
        cum = self.sum_of_all - inv_cum
        return self.cumsum.get(cum, 0)
```

Initial submission, use dict of list
```python
class Solution:
    def subarraySum(self, nums: List[int], k: int) -> int:
        counter = 0
        inv_cum = inv_cumsum()
        # TODO: look init later
        for i in range(len(nums)):
            counter += len(inv_cum.indexes(k - nums[i]))
            if (k - nums[i]) == 0:
                counter += 1
            # update
            inv_cum.append(nums[i])
        return counter
    
class inv_cumsum:
    def __init__(self):
        self.sum_of_all = 0
        self.cumsum = dict() # without current element
        self.i = 0
        
    def append(self, x):
        self.cumsum.setdefault(self.sum_of_all, []).append(self.i)
        self.sum_of_all += x
        self.i += 1
        
    def indexes(self, inv_cum):
        cum = self.sum_of_all - inv_cum
        return self.cumsum.get(cum, [])
```
# Care
- 如果一堆关系搞不清，可以先写一个 class 用于理清关系
- 如果一次想不清，可以先用成本高一些的方法看看大框架能不能行得通，如果行得通可以再 refine。比如这里不知道i有没有用，就先存着，后来发现只需要数目，就用计数器来替代list。