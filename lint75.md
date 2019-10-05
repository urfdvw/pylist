# [75. Find Peak Element](https://www.lintcode.com/problem/find-peak-element/description)
There is an integer array which has the following features:
- The numbers in adjacent positions are different.
- A[0] < A[1] && A[A.length - 2] > A[A.length - 1].

We define a position P is a peak if:
- A[P] > A[P-1] && A[P] > A[P+1]

Find a peak element in this array. Return the index of the peak.

Example 1:
```
Input:  [1, 2, 1, 3, 4, 5, 7, 6]
Output:  1 or 6

Explanation:
return the index of peek.
```

Example 2:
```
Input: [1,2,3,4,1]
Output:  3
```
Challenge
```
Time complexity O(logN)
```
## Solution
```python
class Solution:
    """
    @param A: An integers array.
    @return: return any of peek positions.
    """
    def findPeak(self, A):
        # corner cases
        
        # bisection init
        # from the first to the second last
        up = len(A) - 2
        low = 0
        while(low + 1 < up):
            mid = int((up - low)/2) + low
            if A[mid] < A[mid + 1]:
                # same as A[0] < A[1]
                low = mid
            if A[mid] > A[mid + 1]:
                # same as A[A.length - 2] > A[A.length - 1].
                up = mid
            # if A[mid] == A[mid + 1]:
                # The numbers in adjacent positions are different.
        # because $low$ might be 0, so check $up$ first
        if A[up] > A[up - 1] and A[up] > A[up + 1]:
            #  Return the index of the peak.
            return up
        else:
            return low
```

questions to ask
- Can I assume that the minimum length of the list is 3? Yes!
        
Special care:
- because len(A) >= 3 always true, no corner case input