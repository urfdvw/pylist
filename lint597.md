# [597. Subtree with Maximum Average](https://www.lintcode.com/problem/subtree-with-maximum-average/description)
Given a binary tree, find the subtree with maximum average. Return the root of the subtree.

Example 1
```
Input：
{1,-5,11,1,2,4,-2}
Output：11
Explanation:
The tree is look like this:
     1
   /   \
 -5     11
 / \   /  \
1   2 4    -2 
The average of subtree of 11 is 4.3333, is the maximun.
```
Example 2
```
Input：
{1,-5,11}
Output：11
Explanation:
     1
   /   \
 -5     11
The average of subtree of 1,-5,11 is 2.333,-5,11. So the subtree of 11 is the maximun.
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
    @param root: the root of binary tree
    @return: the root of the maximum average of subtree
    """
    def findSubtree2(self, root):
        def dfs(node):
            """
            in: 
                node: treenode: root of current subtree
            out:
                maxnode: treenode: root of currently known 
                                   subtree with maximum average
                maxmean: float: currently known max average
                n: int: number of nodes in the current subtree
                accu: int: sum of the nodes in the currently subtree
            """
            # if no such node
            if node is None:
                return None, -float("inf"), 0, 0
            # if leaf
            if node.left is None and node.right is None:
                return node, node.val, 1, node.val
            # acquire answers
            maxnodeL, maxmeanL, nL, accuL = dfs(node.left)
            maxnodeR, maxmeanR, nR, accuR = dfs(node.right)
            # combine answers
            ## get the average of the current tree
            ### find current $n$ and $accu$
            n = nL + nR + 1
            accu = accuL + accuR + node.val
            ### find average
            mean = accu / n
            ## update the max record
            maxmean = max([maxmeanL, maxmeanR, mean])
            if maxmean == maxmeanL:
                maxnode = maxnodeL
            elif maxmean == maxmeanR:
                maxnode = maxnodeR
            else:
                maxnode = node
            # return combined answer
            return maxnode, maxmean, n, accu
        
        return dfs(root)[0]
```
Special care:
- 先输出最重要的结果，然后再看为了这个结果还需要什么中间结果
    - 这题要哪个subtree的root，所以先输出```maxnode```
    - 为了maxnode必须记录```maxmean```
    - 为了算mean必须记录每个subtree的mean，然而并不能直接从两个mean得到新的mean。所以改为记录```n```和```accu```。
- combine answer的时候从最原材料的变量开始操作。

[Binary tree notes](readme.md#Binary-Tree)