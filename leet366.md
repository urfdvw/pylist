# 366. Find Leaves of Binary Tree

# Solution

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def findLeaves(self, root: Optional[TreeNode]) -> List[List[int]]:
        dist_list = self.dfs(root)[0]
        keys = sorted(list(dist_list.keys()))
        return [dist_list[k] for k in keys]
        
    def dfs(self, node):
        if node is None:
            return dict(), -float('inf')
        if node.left is None and node.right is None:
            return {0: [node.val]}, 0
        
        ansl, distl = self.dfs(node.left)
        ansr, distr = self.dfs(node.right)
        
        dist = max(distl, distr) + 1
        ans = {dist: [node.val]}
        
        for key in ansl:
            ans.setdefault(key, []).extend(ansl[key])
        for key in ansr:
            ans.setdefault(key, []).extend(ansr[key])
        
        return ans, dist # ans, key: distance to leaf, val: [vals]
```

```steps
```