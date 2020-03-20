# [902. Kth Smallest Element in a BST](https://www.lintcode.com/problem/kth-smallest-element-in-a-bst/description)

Given a binary search tree, write a function kthSmallest to find the kth smallest element in it.

You may assume k is always valid, 1 ≤ k ≤ BST's total elements.

Example 1:
```
Input：{1,#,2},2
Output：2
Explanation：
	1
	 \
	  2
The second smallest element is 2.
```
Example 2:
```
Input：{2,1,3},1
Output：1
Explanation：
  2
 / \
1   3
The first smallest element is 1.
```
# solution
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
    @param k: the given k
    @return: the kth smallest element in BST
    """
    def kthSmallest(self, root, k):
        inorder = self.dfs(root, k)
        return inorder[k-1]
        
    """
    inorder: return incomplete inorder 
    """
    def dfs(self, node, k):
        # if edge
        if node is None:
            return []
        # if leaf
        if node.left is None and node.right is None:
            return [node.val]
        # acquire answer
        llist = self.dfs(node.left, k)
        if len(llist) >= k:
            return llist
        rlist = self.dfs(node.right, k-len(llist)-1)
        return llist + [node.val] + rlist
```

# Special care
- 这个题目比较特别，因为是左右不平衡的。如果在左边满足了要求的，右边可以不看。所以左边的答案得到了以后，先判断，如果还需要右边，再计算右边。而且右边的递归大小k也减小了。