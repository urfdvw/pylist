# [595. Binary Tree Longest Consecutive Sequence](https://www.lintcode.com/problem/binary-tree-longest-consecutive-sequence/description)
Given a binary tree, find the length of the longest consecutive sequence path.

The path refers to any sequence of nodes from some starting node to any node in the tree along the parent-child connections. The longest consecutive path need to be from parent to child (cannot be the reverse).

Example 1:
```
Input:
   1
    \
     3
    / \
   2   4
        \
         5
Output:3
Explanation:
Longest consecutive sequence path is 3-4-5, so return 3.
```
Example 2:
```
Input:
   2
    \
     3
    / 
   2    
  / 
 1
Output:2
Explanation:
Longest consecutive sequence path is 2-3,not 3-2-1, so return 2.
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
    @param root: the root of binary tree
    @return: the length of the longest consecutive sequence path
    """
    def longestConsecutive(self, root):
        def dfs(node):
            """
            output:
                maxlength: int: length of currently known LCS
                length: int: length of a LCS from botton to here
            """
            # if no such node:
            if node is None:
                return 0, 0
            # if leaf
            if node.left is None and node.right is None:
                return 1, 1
            # acquire answers
            maxlengthL, lengthL = dfs(node.left)
            maxlengthR, lengthR = dfs(node.right)
            # combine answer
            ## update length
            length = 1  # at least you have this current node
            if node.left is not None:
                if node.val == node.left.val - 1:
                    length = max([length, lengthL + 1])
            if node.right is not None:
                if node.val == node.right.val - 1:
                    length = max([length, lengthR + 1])
            ## update max length
            maxlength = max([maxlengthL, maxlengthR, length])
            # return combined answer
            return maxlength, length
        
        return dfs(root)[0]
```
special care
- the least number of counting is ```0```, no need to have the default as ```-float('inf')```.
- for syntax, be care for '-th', ':', '=='