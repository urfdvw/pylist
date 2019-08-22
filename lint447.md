# [447. Search in a Big Sorted Array](https://www.lintcode.com/problem/search-in-a-big-sorted-array/description)

Given a big sorted array with non-negative integers sorted by non-decreasing order. The array is so big so that you can not get the length of the whole array directly, and you can only access the kth number by ArrayReader.get(k) (or ArrayReader->get(k) for C++).

Find the first index of a target number. Your algorithm should be in O(log k), where k is the first index of the target number.

Return -1, if the number doesn't exist in the array.

Example 1:
```
Input: [1, 3, 6, 9, 21, ...], target = 3
Output: 1
```
Example 2:
```
Input: [1, 3, 6, 9, 21, ...], target = 4
Output: -1
```
Challenge
```
O(logn) time, n is the first index of the given target number.
```
## Solution:
```python
"""
Definition of ArrayReader
class ArrayReader(object):
    def get(self, index):
        # return the number on given index, 
        # return 9223372036854775807 if the index is invalid.
"""
class Solution:
    """
    @param: reader: An instance of ArrayReader.
    @param: target: An integer
    @return: An integer which is the first index of target.
    """
    def searchBigSortedArray(self, reader, target):
        # corner case less than 2 elements
        ## len == 0
        if reader.get(0) == 9223372036854775807:
            return -1
        ## len == 1 
        if reader.get(1) == 9223372036854775807:
            if reader.get(0) == target:
                return 0
            else:
                return -1
        # init up and low
        ## init up to cover target
        up = 1
        while not reader.get(up) == 9223372036854775807:
            if reader.get(up) > target:
                break
            up *= 2
        ## init low t0 not cover target
        low = up // 2
        while not reader.get(low) < target:
            if low == 0:
                break
            low //= 2
        while low < up - 1:
            # while low and up are not next to each other
            mid = int((up - low)/2 + low)
            if reader.get(mid) == 9223372036854775807 or reader.get(mid) > target:
                up = mid
            if reader.get(mid) < target:
                low = mid
            if reader.get(mid) == target:
                up = mid
        # check up or low
        ## first, then low first
        if reader.get(low) == target:
            return low
        if reader.get(up) == target:
            return up
        # if not found
        return -1
```
Special care:
- without ```if low == 0:```, the while will catch dead loop, when ```reader.get(0)``` gives the target

A much simpler solution without increase the time complexity too much.
no need for comparing the target when getting the range.

```python
"""
Definition of ArrayReader
class ArrayReader(object):
    def get(self, index):
    	# return the number on given index, 
        # return 9223372036854775807 if the index is invalid.
"""
class Solution:
    """
    @param: reader: An instance of ArrayReader.
    @param: target: An integer
    @return: An integer which is the first index of target.
    """
    def searchBigSortedArray(self, reader, target):
        # corner case 
        ## len == 0
        if reader.get(0) == 9223372036854775807:
            return -1
        ## len == 1 
        if reader.get(1) == 9223372036854775807:
            if reader.get(0) == target:
                return 0
            else:
                return -1
        # init up and low
        low = 0
        up = 1
        while not reader.get(up) == 9223372036854775807:
            up *= 2
        while low < up - 1:
            # while low and up are not next to each other
            mid = int((up - low)/2 + low)
            if reader.get(mid) == 9223372036854775807 or reader.get(mid) > target:
                up = mid
            if reader.get(mid) < target:
                low = mid
            if reader.get(mid) == target:
                up = mid
        # check up or low
        ## first, then low first
        if reader.get(low) == target:
            return low
        if reader.get(up) == target:
            return up
        # if not found
        return -1
```
special care
- search upper bound from up=1