# "bisect" package examples

## [14. First Position of Target](https://www.lintcode.com/problem/first-position-of-target/description)
```python
import bisect as bs
class Solution:
    """
    @param nums: An integer array sorted in ascending order
    @param target: An integer
    @return: An integer
    """
    def findPosition(self, nums, target):
        # return 0 if empty set
        if not nums:
            return -1
        # find the left-insert position 
        ind = bs.bisect_left(nums, target)
        # if beyond the range return -1
        if(ind == len(nums)):
            return -1
        # check the element on the right hand side of the left-insert position (same index)
        if(nums[ind] == target):
            return ind
        else:
            return -1
```
## [458. Last Position of Target](https://www.lintcode.com/problem/last-position-of-target/description)
```python
import bisect as bs
class Solution:
    """
    @param nums: An integer array sorted in ascending order
    @param target: An integer
    @return: An integer
    """
    def lastPosition(self, nums, target):
        # return -1 on empty set
        if not nums:
            return -1
        # find index by bisect
        ind = bs.bisect_right(nums,target)
        '''
        # return -1 if insert right at beginning
        if ind == 0:
            return -1
        ''' # this section can be conbined into next setp
        # return -1 if not found
        if nums[ind-1] == target:
            return ind-1
        else:
            return -1
```
## special care
- if the target exist in the list, left-insert position is the index of found target
- For first, use bisect_left(); for last, use bisect_right().