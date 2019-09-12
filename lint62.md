# [62. Search in Rotated Sorted Array](https://www.lintcode.com/problem/search-in-rotated-sorted-array/description)
Suppose a sorted array is rotated at some pivot unknown to you beforehand.

(i.e., 0 1 2 4 5 6 7 might become 4 5 6 7 0 1 2).

You are given a target value to search. If found in the array return its index, otherwise return -1.

You may assume no duplicate exists in the array.

Example 1:
```
Input: [4, 5, 1, 2, 3] and target=1, 
Output: 2.
```
Example 2:
```
Input: [4, 5, 1, 2, 3] and target=0, 
Output: -1.
```
Challenge
```
O(logN) time
```
## solution
```python
class Solution:
    """
    @param A: an integer rotated sorted array
    @param target: an integer to be searched
    @return: an integer
    """
    def search(self, A, target):
        # corner cases
        if len(A) == 0:
            return -1
        if len(A) == 1:
            if A[0] == target:
                return 0
            else:
                return -1
        # init up and low
        up = len(A)-1
        low = 0
        # bisection loop
        while low + 1 < up:
            mid = int((up - low)/2) + low
            if A[low] < A[mid]:
                if A[low] <= target and target <= A[mid]:
                    up = mid
                else:
                    low = mid
            if A[mid] < A[up]:
                if A[mid] <= target and target <= A[up]:
                    low = mid
                else:
                    up = mid
        # check up or low, because no duplication, order does not matter
        if A[up] == target:
            return up
        elif A[low] == target:
            return low
        else:
            return -1
```
Special care:
- When compare elements in A, use ">" or "<", because no duplication
- When compare target with elements in A, use ">=" or "<="