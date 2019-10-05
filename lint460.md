# [460. Find K Closest Elements](https://www.lintcode.com/problem/find-k-closest-elements/description)

Given target, a non-negative integer k and an integer array A sorted in ascending order, find the k closest numbers to target in A, sorted in ascending order by the difference between the number and target. Otherwise, sorted in ascending order by number if the difference is same.
- The value k is a non-negative integer and will always be smaller than the length of the sorted array.
- Length of the given array is positive and will not exceed 10^4
- Absolute value of elements in the array will not exceed 10^4
Example 1:
```
Input: A = [1, 2, 3], target = 2, k = 3
Output: [2, 1, 3]
```
Example 2:
```
Input: A = [1, 4, 6, 8], target = 3, k = 3
Output: [4, 1, 6]
```
Challenge
```
O(logn + k) time
```

## Solution
```python
class Solution:
    """
    @param A: an integer array
    @param target: An integer
    @param k: An integer
    @return: an integer array
    """
    def kClosestNumbers(self, A, target, k):
        # init 
        up = len(A)
        low = 0
        # binary search
        while low + 1 < up:
            mid = (low + up) // 2
            if A[mid] > target:
                up = mid
            if A[mid] < target:
                low = mid
            if A[mid] == target:
                up = mid + 1
                low = mid 
                break
        # use up and low as kappa pointers
        ans = []
        while len(ans) < k:
            # if one pointer cannot move, move the other
            if not self.inbond(A, low):
                ans.append(A[up])
                up += 1
                continue
            if not self.inbond(A, up):
                ans.append(A[low])
                low -= 1
                continue
            # move the closer one
            if target - A[low] <= A[up] - target:
                ans.append(A[low])
                low -= 1
            else:
                ans.append(A[up])
                up += 1
        return ans

    def inbond(self, A, i):
        if i < 0 or i >= len(A):
            return False
        return True
```

special care
- is **find any position of target** case, because second half of code doesen't care where to start from.
- ```up = mid + 1``` because ```mid``` is never the last index