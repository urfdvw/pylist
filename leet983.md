# [983. Minimum Cost For Tickets](https://leetcode.com/problems/minimum-cost-for-tickets/)

In a country popular for train travel, you have planned some train travelling one year in advance.  The days of the year that you will travel is given as an array days.  Each day is an integer from 1 to 365.

Train tickets are sold in 3 different ways:
- a 1-day pass is sold for costs[0] dollars;
- a 7-day pass is sold for costs[1] dollars;
- a 30-day pass is sold for costs[2] dollars.

The passes allow that many days of consecutive travel.  For example, if we get a 7-day pass on day 2, then we can travel for 7 days: day 2, 3, 4, 5, 6, 7, and 8.

Return the minimum number of dollars you need to travel every day in the given list of days.

Example 1:

    Input: days = [1,4,6,7,8,20], costs = [2,7,15]
    Output: 11
    Explanation: 
    For example, here is one way to buy passes that lets you travel your travel plan:
    On day 1, you bought a 1-day pass for costs[0] = $2, which covered day 1.
    On day 3, you bought a 7-day pass for costs[1] = $7, which covered days 3, 4, ..., 9.
    On day 20, you bought a 1-day pass for costs[0] = $2, which covered day 20.
    In total you spent $11 and covered all the days of your travel.
Example 2:

    Input: days = [1,2,3,4,5,6,7,8,9,10,30,31], costs = [2,7,15]
    Output: 17
    Explanation: 
    For example, here is one way to buy passes that lets you travel your travel plan:
    On day 1, you bought a 30-day pass for costs[2] = $15 which covered days 1, 2, ..., 30.
    On day 31, you bought a 1-day pass for costs[0] = $2 which covered day 31.
    In total you spent $17 and covered all the days of your travel.

# Solutions
```python
from functools import lru_cache
class Solution:
    def mincostTickets(self, days: List[int], costs: List[int]) -> int:
        self.costs = costs
        self.ranges = [1, 7, 30]
        self.days = days
        return self.dc(len(days))
        
    @lru_cache
    def dc(self, n):
        """
        return the minimum money needed for the first n days' travel
        """
        # return
        if n == 0:
            return 0
        
        # recursion
        min_money = float('inf')
        for i in range(3):
            min_money = min(min_money, self.dc(self.devide(n, self.ranges[i])) + self.costs[i])
        
        return min_money
    
    def devide(self, n, r):
        """
        return the number of days that does not include the last r dates in the first n days.
        """
        for i in range(n-1, 0, -1):
            # print('n', n, 'r', r, 'i', i, self.days[n-1], self.days[i-1])
            if self.days[i-1] < self.days[n-1] - r + 1:
                return i
        return 0
```

A faster implementation of `devide` can be achieved by bisect.

```python
from bisect import bisect_left

...

class Solution:

    ...

    def devide(self, n, r):
        """
        return the number of days that does not include the last r dates in the first n days.
        """
        return bisect_left(self.days, self.days[n-1] - r + 1, hi=n-1)
```