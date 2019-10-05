# [749. John's backyard garden](https://www.lintcode.com/problem/johns-backyard-garden/description?_from=ladder&&fromId=92)

John wants to build a back garden on the empty space behind his home. There are two kinds of bricks now, one is 3 dm high and the other is 7 dm high. John wants to enclose a high x dm wall. If John can do this, output YES, otherwise NO.

Example 1:
```
Input : x = 10
Output : "YES"
Explanation :
x = 3 + 7:That is, you need one batch of 3 dm height bricks and one batch of 7 dm height bricks.
```
Example 2:
```
Input : x = 5
Output : "NO"
Explanation:
John can not enclose a high 5 dm wall with 3 dm height bricks and 7 dm height bricks.
```
Example 3:
```
Input : x = 13
Output : "YES"
Explanation :
x = 2 * 3 + 7:That is, you need two batch of 3 dm height bricks and one batch of 7 dm height bricks.
```
## Solution
```python
class Solution:
    """
    @param x: the wall's height
    @return: YES or NO
    """
    def isBuild(self, x):
        brick = [3, 7]
        # dp[i][y]
        # first i kinds of bricks
        # if wall ends at y
        dp = [[False]*(x+1) for i in range(len(brick)+1)]
        dp[0][0] = True
        for i in range(1, len(dp)):
            for y in range(len(dp[0])):
                if y < brick[i-1]:
                    dp[i][y] = dp[i-1][y]
                else:
                    dp[i][y] = dp[i-1][y] or dp[i][y-brick[i-1]]
        if dp[-1][-1]:
            return "YES"
        else:
            return "NO"
```