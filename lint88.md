# [88. Lowest Common Ancestor of a Binary Tree](https://www.lintcode.com/problem/lowest-common-ancestor-of-a-binary-tree/description)

Given the root and two nodes in a Binary Tree. Find the lowest common ancestor(LCA) of the two nodes.

The lowest common ancestor is the node with largest depth which is the ancestor of both nodes.

Assume two nodes are exist in tree.

Example 1:
```
Input：{1},1,1
Output：1
Explanation：
 For the following binary tree（only one node）:
         1
 LCA(1,1) = 1
```
Example 2:
```
Input：{4,3,7,#,#,5,6},3,5
Output：4
Explanation：
 For the following binary tree:

      4
     / \
    3   7
       / \
      5   6
			
 LCA(3, 5) = 4
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
    @param: root: The root of the binary search tree.
    @param: A: A TreeNode in a Binary.
    @param: B: A TreeNode in a Binary.
    @return: Return the least common ancestor(LCA) of the two nodes.
    """
    def lowestCommonAncestor(self, root, A, B):
        # questions to ask
        ## what does ancestor means? node or node value?
        ### I guess node here
        def dfs(node):
            """
            in:
                node: treenode: root of current subtree
            out:
                lcaRecord: node: the LCA looking for if found
                    None if not found
                hasA: bool: A is included in the subtree
                hasB: bool: B is included in the subtree
            """
            # if no such node
            if node is None:
                return None, False, False
            # if leaf
            if node.left is None and node.right is None:
                hasA = node is A
                hasB = node is B
                if hasA and hasB:
                    lcaRecord = node
                else:
                    lcaRecord = None
                return lcaRecord, hasA, hasB
            # get answers
            lcaRecordL, hasAL, hasBL = dfs(node.left)
            lcaRecordR, hasAR, hasBR = dfs(node.right)
            # combine answer
            ## if LCA found, then copy the answer
            if lcaRecordL is not None:
                return lcaRecordL, hasAL, hasBL
            if lcaRecordR is not None:
                return lcaRecordR, hasAR, hasBR
            ## if not found yet, see if it is here
            hasA = hasAL or hasAR or node is A
            hasB = hasBL or hasBR or node is B
            if hasA and hasB:
                return node, hasA, hasB
            else:
                return None, hasA, hasB
        
        return dfs(root)[0]
```
special care
- once the answer is found, there is no need for any calculation.
So the first step in 'combine answers' is check if answer is already found

[Binary tree notes](readme.md#Binary-Tree)