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
            
        # call recursion
        paths = self.dfs(root)
        pathswords = ['->'.join(l[::-1]) for l in paths]
        return pathswords
        
    def dfs(self, node):
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
        pathsLeft = self.dfs(node.left)
        pathsRight = self.dfs(node.right)
        # conbine answers
        paths = pathsLeft + pathsRight
        for p in paths:
            p.append(str(node.val)) 
        # return conbined answer
        return paths
```
special care
- ```A.insert()``` and ```A.extend()``` do not have return value
- But ```insert(0, )``` is a bad practice. I would rather reverse the list while using the accumulated list
    - ```pathswords = ['->'.join(l[::-1]) for l in paths]``` 
    - and ```p.append(str(node.val))```
    - instead of ```p.insert(0, str(node.val))```
- 如果不是为了得到一个list就别用list comprehension
- [for循环对和inplace 操作](misc/For and List and inplace operation.ipynb)