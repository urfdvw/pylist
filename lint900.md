# [900. Closest Binary Search Tree Value](https://www.lintcode.com/problem/closest-binary-search-tree-value/description)

Given a non-empty binary search tree and a target value, find the value in the BST that is closest to the target.

Given target value is a floating point.
You are guaranteed to have only one unique value in the BST that is closest to the target.

Example1
```
Input: root = {5,4,9,2,#,8,10} and target = 6.124780
Output: 5
Explanation：
Binary tree {5,4,9,2,#,8,10},  denote the following structure:
        5
       / \
     4    9
    /    / \
   2    8  10
```
Example2
```
Input: root = {3,2,4,1} and target = 4.142857
Output: 4
Explanation：
Binary tree {3,2,4,1},  denote the following structure:
     3
    / \
  2    4
 /
1
```
# Solution
```python
"""
Definition of TreeNode:
class TreeNode:
    def __init__(self, val):
        self.val = val
        self.left, self.right = None, None
"""

class Solution:
    
    
    """
    @param root: the given BST
    @param target: the given target
    @return: the value in the BST that is closest to the target
    """
    def closestValue(self, root, target):
        return self.dfs(root, target)[0]
        
    def dfs(self, node, target):
        """
        in:
            same as closestValue
        out:
            val: the value in the BST that is closest to the target
            diff: abs(val - target)
        """
        # no such node
        if node is None:
            return None, float('inf')
        # leaf
        if node.left is None and node.right is None:
            return node.val, abs(node.val - target)
        # acquire answers from subtrees
        val_l, diff_l = self.dfs(node.left, target)
        val_r, diff_r = self.dfs(node.right, target)
        # combine answers
        diff_n = abs(node.val - target)
        diff_min = min([diff_l, diff_r, diff_n])
        if diff_min == diff_n:
            return node.val, diff_n
        if diff_min == diff_l:
            return val_l, diff_l
        if diff_min == diff_r:
            return val_r, diff_r
```
# special care
- 无穷大的python写法`float('inf')`
- 其实只返回值，不返回偏差也没什么问题