# [543. Diameter of Binary Tree](https://leetcode.com/problems/diameter-of-binary-tree/)

Given a binary tree, you need to compute the length of the diameter of the tree. The diameter of a binary tree is the length of the longest path between any two nodes in a tree. This path may or may not pass through the root.

Example:

    Given a binary tree
          1
         / \
        2   3
       / \     
      4   5    
    Return 3, which is the length of the path [4,2,1,3] or [5,2,1,3].

Note: The length of path between two nodes is represented by the number of edges between them.

# Solution
```python
class Solution:
    def diameterOfBinaryTree(self, root: TreeNode) -> int:
        if root is None:
            return 0
        
        return self.dc(root)[0] - 1
        
    def dc(self, node):
        if node is None:
            return 0, 0, 0
        if node.left is None and node.right is None:
            return 1, 1, 1
        
        l_maxpath, l_path, l_depth = self.dc(node.left)
        r_maxpath, r_path, r_depth = self.dc(node.right)
        
        depth = max(l_depth, r_depth) + 1
        path = l_depth + 1 + r_depth
        maxpath = max([path, l_maxpath, r_maxpath])
        
        return maxpath, path, depth
        
        
# nodes on dia path = l_depth + 1 + right_depth
```
# Care
- 二叉树上的分治在检查的时候一定注意：
    - combine的时候有没有充分利用左右获得的答案