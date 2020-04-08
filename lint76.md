# [76. Longest Increasing Subsequence](https://www.lintcode.com/problem/longest-increasing-subsequence/description)

Given a sequence of integers, find the longest increasing subsequence (LIS).

You code should return the length of the LIS.

Example 1:

	Input:  [5,4,1,2,3]
	Output:  3
	
	Explanation:
	LIS is [1,2,3]

Example 2:

	Input: [4,2,4,5,3,7]
	Output:  4
	
	Explanation: 
	LIS is [2,4,5,7]

Challenge

    Time complexity O(n^2) or O(nlogn)

Clarification: What's the definition of longest increasing subsequence?
- The longest increasing subsequence problem is to find a subsequence of a given sequence in which the subsequence's elements are in sorted order, lowest to highest, and in which the subsequence is as long as possible. This subsequence is not necessarily contiguous, or unique.
- https://en.wikipedia.org/wiki/Longest_increasing_subsequence

# solution
```python
from functools import lru_cache
class Solution:
    """
    @param nums: An integer array
    @return: The length of LIS (longest increasing subsequence)
    """
    def longestIncreasingSubsequence(self, nums):
        if len(nums) <= 1:
            return len(nums)
        self.nums = nums
        return max([self.dp(i) for i in range(len(nums))])
            
    @lru_cache(None)
    def dp(self, n):
        if n == 0:
            return 1
        candi = [self.dp(i) for i in range(n) if self.nums[i] < self.nums[n]]
        if len(candi) == 0:
            return 1
        return max(candi) + 1
```

# care
- max([]) can raise error
- the solution might not be the last one, so need to find all and max()