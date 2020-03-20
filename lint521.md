# [521. Remove Duplicate Numbers in Array](https://www.lintcode.com/problem/remove-duplicate-numbers-in-array/description)
Given an array of integers, remove the duplicate numbers in it.

You should:

1. Do it in place in the array.
2. Move the unique numbers to the front of the array.
3. Return the total number of the unique numbers.

Example 1:
```
Input:
nums = [1,3,1,4,4,2]
Output:
[1,3,4,2,?,?]
4
```
Explanation:

- Move duplicate integers to the tail of nums => nums = [1,3,4,2,?,?].
- Return the number of unique integers in nums => 4.
- Actually we don't care about what you place in ?, we only care about the part which has no duplicate integers.

Example 2:
```
Input:
nums = [1,2,3]
Output:
[1,2,3]
3
```
Challenge
```
Do it in O(n) time complexity.
Do it in O(nlogn) time without extra space.
```

# Solution 1

因为是O(nlogn)，所以很可能是排过序然后处理。思路是排序后，如果遇到数字跳变，记录跳变后的第一个数字。

```python
class Solution:
    """
    @param nums: an array of integers
    @return: the number of unique integers
    """
    def deduplication(self, nums):
        # write your code here
        nums.sort()
        if len(nums) == 0:
            return 0
        slower = 1
        for faster in range(1, len(nums)):
            if nums[faster] != nums[faster - 1]:
                nums[slower] = nums[faster]
                slower += 1
        return slower
```

# Solution 2
用set记录算过的数字。时间复杂度因该是O(n)

```python
class Solution:
    """
    @param nums: an array of integers
    @return: the number of unique integers
    """
    def deduplication(self, nums):
        # empty case
        if len(nums) <= 1:
            return len(nums)
        # record unique numbers read
        rec = set()
        write = 0
        for read in range(len(nums)):
            # if a seen number
            if nums[read] in rec:
                continue
            # if not seen
            nums[write] = nums[read]
            rec.add(nums[read])
            write += 1
        return len(rec)
```