# [93. Balanced Binary Tree](https://www.lintcode.com/problem/balanced-binary-tree/description)

Given a binary tree, determine if it is height-balanced.

For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of every node never differ by more than 1.

Example  1:
```
Input: tree = {1,2,3}
Output: true

Explanation:
This is a balanced binary tree.
		  1  
		 / \                
		2   3
```

Example  2:
```
Input: tree = {3,9,20,#,#,15,7}
Output: true

Explanation:
This is a balanced binary tree.
		  3  
		 / \                
		9  20                
		  /  \                
		 15   7 

```

Example  3:
```
Input: tree = {1,#,2,3,4}
Output: false

Explanation:
This is not a balanced tree. 
The height of node 1's right sub-tree is 2 but left sub-tree is 0.
		 1  
		  \                
		   2                
		  / \                
		 3   4
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
    def dfs(self, node):
        """
        in: 
            node: TreeNode: root of subtree
        out
            balanced: bool: if current subtree balanced
            depth: int: depth of current subtree
        """
        # if no such node
        if node is None:
            # empty tree is balanced
            return True, 0
        # if leaf
        if node.left is None and node.right is None:
            return True, 1
        # acquire answer
        BL, DL = dfs(node.left)
        BR, DR = dfs(node.right)
        # combine answer
        depth = max([DL, DR]) + 1
        if not (BL and BR):
            return False, depth
        if abs(DL - DR) > 1:
            return False, depth
        return True, depth
    
    def isBalanced(self, root):
        """
        in:
            root: TreeNode: The root of binary tree.
        out:
            bool: True if this Binary tree is Balanced.
        """
        return self.dfs(root)[0]
```

[Binary tree notes](readme.md#Binary-Tree)