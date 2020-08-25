# [404. Sum of Left Leaves](https://leetcode.com/problems/sum-of-left-leaves/)

Find the sum of all left leaves in a given binary tree.

Example:

        3
       / \
      9  20
        /  \
       15   7

    There are two left leaves in the binary tree, with values 9 and 15 respectively. Return 24.

# Solution
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def sumOfLeftLeaves(self, root: TreeNode) -> int:
        accu, leaf = self.dc(root)
        if leaf:
            return 0
        else:
            return accu
        
    def dc(self, node):
        
        if node is None:
            return 0, False
        
        if node.left is None and node.right is None:
            return node.val, True
        
        acculeft, leafleft = self.dc(node.left)
        accuright, leafright = self.dc(node.right)
        
        accu = acculeft
        if not leafright:
            accu += accuright
            
        leaf = False
        
        return accu, leaf
```