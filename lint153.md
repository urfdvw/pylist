# [153. Combination Sum II](https://www.lintcode.com/problem/combination-sum-ii/description)

Given an array num and a number target. Find all unique combinations in num where the numbers sum to target.

Each number in num can only be used once in one combination.
All numbers (including target) will be positive integers.
Numbers in a combination a1, a2, … , ak must be in non-descending order. (ie, a1 ≤ a2 ≤ … ≤ ak)
Different combinations can be in any order.
The solution set must not contain duplicate combinations.

Example 1:
```
Input: num = [7,1,2,5,1,6,10], target = 8
Output: [[1,1,6],[1,2,5],[1,7],[2,6]]
```
Example 2:
```
Input: num = [1,1,1], target = 2
Output: [[1,1]]
Explanation: The solution set must not contain duplicate combinations.
```

# solution
```python
class Solution:
    """
    @param candidates: A list of integers
    @param target: An integer
    @return: A list of lists of integers
    """
    def combinationSum2(self, candidates, target):
        ans = []
        cur = []
        csum = 0
        self.traverse(sorted(candidates), target, ans, cur, csum)
        return ans
    
    def traverse(self, candidates, target, ans, cur, csum):
        if csum == target:
            ans.append(cur[:])
            return
        if csum > target:
            return
        
        for i, c in enumerate(candidates):
            if i > 0:
                if c == candidates[i-1]:
                    continue
            cur.append(c)
            csum += c
            self.traverse(candidates[i+1:], target, ans, cur, csum)
            csum -= c
            cur.pop()
        return 
```

# [135. Combination Sum](https://www.lintcode.com/problem/combination-sum/description)

Given a set of candidtate numbers candidates and a target number target. Find all unique combinations in candidates where the numbers sums to target.

The same repeated number may be chosen from candidates unlimited number of times.

All numbers (including target) will be positive integers.
Numbers in a combination a1, a2, … , ak must be in non-descending order. (ie, a1 ≤ a2 ≤ … ≤ ak)
Different combinations can be in any order.
The solution set must not contain duplicate combinations.

Example 1
```
Input: candidates = [2, 3, 6, 7], target = 7
Output: [[7], [2, 2, 3]]
```
Example 2:
```
Input: candidates = [1], target = 3
Output: [[1, 1, 1]]
```
## Solution
只有一行的差别。
```python
self.traverse(candidates[i:], target, ans, cur, csum)
```

# care
- 先排序的原因
    - 答案要求每项排好序
    - 用相邻相等检测重复
- 关于递归调用时候scale的控制
    - 如果递归调用的时候用`candidates[i+1:]`，意思是本元素不再参与下一层递归。意思是元素不能重复使用
    - 如果是`candidates[i:]`，意思是本元素可以重复使用。
    - 然而较小的元素永远不会包含，是为了避免答案重复