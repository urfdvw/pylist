# [95. Validate Binary Search Tree](https://www.lintcode.com/problem/validate-binary-search-tree/description)
Given a binary tree, determine if it is a valid binary search tree (BST).

Assume a BST is defined as follows:
- The left subtree of a node contains only nodes with keys less than the node's key.
- The right subtree of a node contains only nodes with keys greater than the node's key.
- Both the left and right subtrees must also be binary search trees.
- A single node tree is a BST

Example 1:
```
Input:  {-1}
Output：true
Explanation：
For the following binary tree（only one node）:
	      -1
This is a binary search tree.
```
Example 2:
```
Input:  {2,1,4,#,#,3,5}
Output: true
For the following binary tree:
	  2
	 / \
	1   4
	   / \
	  3   5
This is a binary search tree.
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
    @return: True if the binary tree is BST, or false
    """
    def isValidBST(self, root):
        def dfs(node):
            """
            in:
                node: treenode: root of current subtree
            out:
                isBST: bool: is True if current subtree is valid BST
                maxVal: int, max value of current subtree
                minVal: int, min ...
            """
            # if no such node
            ## BST is not guaranteed full
            if node is None:
                return True, -float('inf'), float('inf')
            # if leaf
            if node.left is None and node.right is None:
                return True, node.val, node.val
            # acquire answers
            isBSTL, maxValL, minValL = dfs(node.left)
            isBSTR, maxValR, minValR = dfs(node.right)
            # combine answer
            ## if already not BST
            if not (isBSTL and isBSTR):
                return False, 0, 0  # value is not important now
            ## update isBST
            if maxValL < node.val and node.val < minValR:
                isBST = True
            else:
                isBST = False
            ## update max and min value
            maxVal = max([maxValL, maxValR, node.val])
            minVal = min([minValL, minValR, node.val])
            # return combined answer
            return isBST, maxVal, minVal
        return dfs(root)[0]
```
special care:
- BST is not guaranteed full
- definition of BST might differ

[Binary tree notes](readme.md#Binary-Tree)