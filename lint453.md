# [453. Flatten Binary Tree to Linked List](https://www.lintcode.com/problem/flatten-binary-tree-to-linked-list/description)

Flatten a binary tree to a fake "linked list" in pre-order traversal.

Here we use the right pointer in TreeNode as the next pointer in ListNode.

Don't forget to mark the left child of each node to null. Or you will get Time Limit Exceeded or Memory Limit Exceeded.

Example 1:
```
Input:{1,2,5,3,4,#,6}
Output：{1,#,2,#,3,#,4,#,5,#,6}
Explanation：
     1
    / \
   2   5
  / \   \
 3   4   6

1
 \
  2
   \
    3
     \
      4
       \
        5
         \
          6
```
Example 2:
```
Input:{1}
Output:{1}
Explanation：
         1
         1
```
Challenge
```
Do it in-place without any extra memory.
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
    @param root: a TreeNode, the root of the binary tree
    @return: nothing
    """
    def flatten(self, root):
        def dfs(node):
            """
            in:
                node: treenode: root of the current subtree
            out:
                # I guess if I can do in-place operation
                nodein: treenode: root of fake linked list
                nodeout: treenode: leaf of fake linked list
            """
            # if no such node
            if node is None:
                return None, None
            # if leaf
            if node.left is None and node.right is None:
                return node, node
            # acquire answers
            inL, outL = dfs(node.left)
            inR, outR = dfs(node.right)
            # combine answers
            ## clean left side
            node.left = None
            ## init outputs
            nodein = node
            nodeout = node
            ## combine sides one-by-one,
            if inL is not None:  # if not the boarder of extended tree
                nodeout.right = inL
                nodeout = outL
            if inR is not None:
                nodeout.right = inR
                nodeout = outR
            # return combined answer
            return nodein, nodeout
        
        dfs(root)
        return

```

special care
- 因为在这个例子中，增广二叉树的边缘并不能参与运算，所以就用None代表特例。在使用时候，先用 ```if A is not None```来判断是否碰到了增广二叉树边缘，如果是边缘，则忽略不做操作。
