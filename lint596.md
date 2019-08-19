# [596. Minimum Subtree](https://www.lintcode.com/problem/minimum-subtree/description)

Given a binary tree, find the subtree with minimum sum. Return the root of the subtree.
Example 1:
```
Input:
{1,-5,2,1,2,-4,-5}
Output:1
Explanation:
The tree is look like this:
     1
   /   \
 -5     2
 / \   /  \
1   2 -4  -5 
The sum of whole tree is minimum, so return the root.
```
Example 2:
```
Input:
{1}
Output:1
Explanation:
The tree is look like this:
   1
There is one and only one subtree in the tree. So we return 1.
```
## solution
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
    @param root: the root of binary tree
    @return: the root of the minimum subtree
    """
    def findSubtree(self, root):
        def dfs(node):
            """
            in: node: node: root of subtree
            out: accu: int: sum of the subtree
            out: minsum: int: min sum of the subtree
            out: minnode: node: root of subtree that have minsum
            """
            # if no such node
            if node is None:
                return 0, float("inf"), None
            # if leaf
            if node.left is None and node.right is None:
                return node.val, node.val, node
            # find results
            accul, minsuml, minnodel = dfs(node.left)
            accur, minsumr, minnoder = dfs(node.right)
            # combine results
            accu = accul + accur + node.val
            minsum = min([minsuml, minsumr, accu])
            if minsum == minsuml:
                minnode = minnodel
            elif minsum == minsumr:
                minnode = minnoder
            else:
                minnode = node
            # return combined answer
            return accu, minsum, minnode
        return dfs(root)[2]  # only minnode is needed
```

special care:
- ```float("inf")``` is how you define the largest float number

[Binary tree notes](readme.md#Binary-Tree)