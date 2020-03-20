# [578. Lowest Common Ancestor III](https://www.lintcode.com/problem/lowest-common-ancestor-iii/description)

Given the root and two nodes in a Binary Tree. Find the lowest common ancestor(LCA) of the two nodes.
The lowest common ancestor is the node with largest depth which is the ancestor of both nodes.

Return null if LCA does not exist.

node A or node B may not exist in tree.

Each node has a different value

Example1
```
Input: 
{4, 3, 7, #, #, 5, 6}
3 5
5 6
6 7 
5 8
Output: 
4
7
7
null
Explanation:
  4
 / \
3   7
   / \
  5   6

LCA(3, 5) = 4
LCA(5, 6) = 7
LCA(6, 7) = 7
LCA(5, 8) = null
```
Example2
```
Input:
{1}
1 1
Output: 
1
Explanation:
The tree is just a node, whose value is 1.
```
# Solution
```python
"""
Definition of TreeNode:
class TreeNode:
    def __init__(self, val):
        this.val = val
        this.left, this.right = None, None
"""
class Solution:
    """
    @param: root: The root of the binary tree.
    @param: A: A TreeNode
    @param: B: A TreeNode
    @return: Return the LCA of the two nodes.
    """
    def lowestCommonAncestor3(self, root, A, B):
        return self.dfs(root, A, B)[0]
        
    def dfs(self, node, A, B):
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
        lcaRecordL, hasAL, hasBL = self.dfs(node.left, A, B)
        lcaRecordR, hasAR, hasBR = self.dfs(node.right, A, B)
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
```