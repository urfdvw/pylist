# [480. Binary Tree Paths](https://www.lintcode.com/problem/binary-tree-paths/description)

Given a binary tree, return all root-to-leaf paths.

Example 1:
```
Input：{1,2,3,#,5}
Output：["1->2->5","1->3"]
Explanation：
   1
 /   \
2     3
 \
  5
```
Example 2:
```
Input：{1,2}
Output：["1->2"]
Explanation：
   1
 /   
2     
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
    @param root: the root of the binary tree
    @return: all root-to-leaf paths
    """
    def binaryTreePaths(self, root):
        def dfs(node):
            """
            in: node: TreeNode
            out: paths: list of list of values, each sublist is a path
            """
            # if no such a node:
            if node is None:
                return []
            # return condition
            if node.left is None and node.right is None:
                return [[str(node.val)]]
            # get answers
            pathsLeft = dfs(node.left)
            pathsRight = dfs(node.right)
            # conbine answers
            paths = []
            paths.extend(pathsLeft)
            paths.extend(pathsRight)
            [p.insert(0, str(node.val)) for p in paths]
            # return conbined answer
            return paths
            
        # call recursion
        paths = dfs(root)
        pathswords = ['->'.join(l) for l in paths]
        return pathswords
```
special care
- ```A.insert()``` and ```A.extend()``` do not have return value

[Binary tree notes](readme.md#Binary-Tree)