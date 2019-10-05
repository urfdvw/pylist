# [69. Binary Tree Level Order Traversal](https://www.lintcode.com/problem/binary-tree-level-order-traversal/description)
Given a binary tree, return the level order traversal of its nodes' ***values***. (ie, from left to right, level by level).

The first data is the root node, followed by the value of the left and right son nodes, and "#" indicates that there is no child node.
The number of nodes does not exceed 20.

Example 1:
```
Input：{1,2,3}
Output：[[1],[2,3]]
Explanation：
  1
 / \
2   3
it will be serialized {1,2,3}
level order traversal
```
Example 2:
```
Input：{1,#,2,3}
Output：[[1],[2],[3]]
Explanation：
1
 \
  2
 /
3
it will be serialized {1,#,2,3}
level order traversal
```
Challenge
```
Challenge 1: Using only 1 queue to implement it.
Challenge 2: Use BFS algorithm to do it.
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
    @param root: A Tree
    @return: Level order a list of lists of integer
    """
    def levelOrder(self, root):
        # corner case:
        if root is None:
            # if insane empty set
            return []
        # init: queue with root
        queue = collections.deque([root])
        # BSF loop
        ans = []
        while queue:
            # while queue is not empty
            layer = []
            for i in range(len(queue)):
                # for each node in current pending layer
                node = queue.popleft()
                # offer children if exist
                if node.left is not None:
                    queue.append(node.left)
                if node.right is not None:
                    queue.append(node.right)
                # main logic
                ## Problem discription is not clear,
                ## should return values instead of node value
                layer.append(node.val)
            ans.append(layer)
        return ans
```

special care:
- lint code always have that insane empty set
- always ask return value or return node reference
- ```sizeOfPendingLayer``` need not to be measured before the for loop