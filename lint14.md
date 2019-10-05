# [14. First Position of Target](https://www.lintcode.com/problem/first-position-of-target/description)
For a given sorted array (ascending order) and a target number, find the ***first*** index of this number in O(log n) time complexity.

If the target number does not exist in the array, return -1.

Example 1:
```
Input:  [1,4,4,5,7,7,8,9,9,10]，1
Output: 0

Explanation: 
the first index of  1 is 0.
```
Example 2:
```
Input: [1, 2, 3, 3, 4, 5, 10]，3
Output: 2

Explanation: 
the first index of 3 is 2.
```
Example 3:
```
Input: [1, 2, 3, 3, 4, 5, 10]，6
Output: -1

Explanation: 
Not exist 6 in array.
```

Challenge
```
If the count of numbers is bigger than 2^32, can your code work properly?
```
## Solution
```python
class Solution:
    """
    @param nums: An integer array sorted in ascending order
    @param target: An integer
    @return: An integer
    """
    def binarySearch(self, nums, target):
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
                # because 'first', mid may be smaller
                up = mid
            elif nums[mid] > target:
                up = mid
            else:  # (nums[mid] < target)
                low = mid
        # check wether up or low
        # because 'first', check the smaller one first
        if nums[low] == target:
            return low
        if nums[up] == target:
            return up
        # if not found
        return -1
```