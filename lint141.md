# [141. Sqrt(x)](https://www.lintcode.com/problem/sqrtx/description)
Implement int sqrt(int x).

Compute and return the square root of x.


Example 1:
```
Input:  0
Output: 0
```

Example 2:
```
Input:  3
Output: 1

Explanation:
return the largest integer y that y*y <= x. 
```
Example 3:
```
Input:  4
Output: 2
```

Challenge
```
O(log(x))
```

## Solution
binary search by condition
```python
class Solution:
    """
    @param x: An integer
    @return: The sqrt of x
    """
    def sqrt(self, x):
        # corner cases
        ## if set is too small for binary search
        if x == 0:
            return 0
        if x == 1:
            return 1
        # condation, con(low) = true
        def con(y): return y*y <= x
        # init up and low bounds
        up = 2
        while con(up):
            up *= 2
            # end with the first y not satisfy condition
        low = int(up / 2)
        # bisection loop
        while up > low + 1:
            # search, while up and low not next to each other
            mid = int(low + (up - low)/2)
            if con(mid):
                low = mid
            else:
                up = mid
        # return the largest integer satisfy condition
        return low
```

special care:
- In the last step, check ```up``` first,
because low will always satisfy ```low * low <= x```,
no matter it is the solution or not.

[Binary search notes](readme.md#Binary-search)

---

## Archived solution

```python
class Solution:
    """
    @param x: An integer
    @return: The sqrt of x
    """
    def sqrt(self, x):
        # corner cases
        ## if set is too small for binary search
        if x == 0:
            return 0
        if x == 1:
            return 1
        # init up and low bounds
        up = 2
        while up * up < x:
            up *= 2
        low = int(up / 2)
        while up > low + 1:
            # search, while up and low not next to each other
            mid = int(low + (up - low)/2)
            if mid * mid > x:
                up = mid
            elif mid * mid == x:
                # becuse x is unique for a given sqrt(x)
                return mid
            else:
                low = mid
        # check if up or low
        ## largest, so check up first
        if up * up <= x:
            return up
        else:
            return low
```
