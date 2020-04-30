# [124. Binary Tree Maximum Path Sum](https://leetcode.com/problems/binary-tree-maximum-path-sum/)

Given a non-empty binary tree, find the maximum path sum.

For this problem, a path is defined as any sequence of nodes from some starting node to any node in the tree along the parent-child connections. The path must contain at least one node and does not need to go through the root.

Example 1:

    Input: [1,2,3]

         1
        / \
       2   3

Output: 6
Example 2:

    Input: [-10,9,20,null,null,15,7]

       -10
       / \
      9  20
        /  \
       15   7

Output: 42

# Solution
refined solution using counter

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def maxPathSum(self, root: TreeNode) -> int:
        return self.dc(root)[0]
        
    def dc(self, node):
        """
        in:
            node: TreeNode: root of sub tree
        out:
            max_sum: the max sum of path within this sub tree
            straight_sums: max of the sums of paths that end at current node including the root
        """
        
        if node is None:
            return -float("inf"), -float("inf")
            
        if node.left is None and node.right is None:
            return node.val, node.val
        
        max_sum_l, max_straight_sums_l = self.dc(node.left)
        max_sum_r, max_straight_sums_r = self.dc(node.right)
        
        max_sum_node = node.val
        if max_straight_sums_l > 0:
            max_sum_node += max_straight_sums_l
        
        if max_straight_sums_r > 0:
            max_sum_node += max_straight_sums_r
            
        max_sum = max([max_sum_l, max_sum_r, max_sum_node])
        
        max_straight_sums = max([node.val, node.val + max_straight_sums_l, node.val + max_straight_sums_r])
        
        return max_sum, max_straight_sums
        
```

initial solution using list

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def maxPathSum(self, root: TreeNode) -> int:
        return self.dc(root)[0]
        
    def dc(self, node):
        """
        in:
            node: TreeNode: root of sub tree
        out:
            max_sum: the max sum of path within this sub tree
            straight_sums: list: the sums of paths that end at current node including the root
        """
        
        if node is None:
            return -float("inf"), []
            
        if node.left is None and node.right is None:
            return node.val, [node.val] 
        
        max_sum_l, straight_sums_l = self.dc(node.left)
        max_sum_r, straight_sums_r = self.dc(node.right)
        
        max_sum_node = node.val
        max_straight_sums_l = self.max(straight_sums_l)
        if max_straight_sums_l > 0:
            max_sum_node += max_straight_sums_l
        
        max_straight_sums_r = self.max(straight_sums_r)
        if max_straight_sums_r > 0:
            max_sum_node += max_straight_sums_r
            
        max_sum = max([max_sum_l, max_sum_r, max_sum_node])
        
        straight_sums = [node.val]
        straight_sums += [node.val + s for s in straight_sums_l]
        straight_sums += [node.val + s for s in straight_sums_r]
        
        return max_sum, straight_sums
    
    def max(self, l):
        if len(l) == 0:
            return -float('inf')
        else:
            return max(l)
        
```
# Care
- 这题的要点在于把每个节点都当作一条path的终点。而不是只考虑叶节点
- 这题也是先用 list 想然后用 counter 优化