# [97. Maximum Depth of Binary Tree](https://www.lintcode.com/problem/maximum-depth-of-binary-tree/description)

Given a binary tree, find its maximum depth.

The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

Example 1:
```
Input: tree = {}
Output: 0
Explanation: The height of empty tree is 0.
```
Example 2:
```
Input: tree = {1,2,3,#,#,4,5}
Output: 3	
Explanation: Like this:
   1
  / \                
 2   3                
    / \                
   4   5
it will be serialized {1,2,3,#,#,4,5}
```
## Solution
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
    @param root: The root of binary tree.
    @return: An integer
    """
    def maxDepth(self, root):
        return self.dfs(root)
        
    def dfs(self, node):
        # if no such node
        if node is None:
            return 0
        # if leaf
        ## this section is not nesessary,
        ## but because this problem is too special
        ## I keep it to fit the template
        if node.left is None and node.right is None:
            return 1
        # get answers from left and right
        depthLeft = self.dfs(node.left)
        depthRight = self.dfs(node.right)
        # combine answers
        depth = max([depthLeft, depthRight]) + 1
        # return combined answer
        return depth
```
special care
- this section is not nesessary, but because this problem is too special. I keep it to fit the template.
- empty tree have 0 layer, and leaf have 1 layer.