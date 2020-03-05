# [614. Binary Tree Longest Consecutive Sequence II](https://www.lintcode.com/problem/binary-tree-longest-consecutive-sequence-ii/description)

Given a binary tree, find the length(number of nodes) of the longest consecutive sequence(Monotonic and adjacent node values differ by 1) path.
The path could be start and end at any node in the tree

Example 1:
```
Input:
{1,2,0,3}
Output:
4
Explanation:
    1
   / \
  2   0
 /
3
0-1-2-3
```
Example 2:
```
Input:
{3,2,2}
Output:
2
Explanation:
    3
   / \
  2   2
2-3
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
    @return: the length of the longest consecutive sequence path
    """
    def longestConsecutive2(self, root):
        def dfs(node):
            """
            in:
                node: TreeNode: root of current sub-tree
            out:
                maxLength: int: the longest length of currently seen 
                    consecutive sequence path
                lenIn: int: the length of increasing sequence including the node
                    increasing means child.val + 1 == node.val
                lenDe: int: the length of decreasing sequence including the node
            """
            # if no such node
            if node is None:
                return -float("inf"), 0, 0
            # if leaf
            if node.left is None and node.right is None:
                return 1, 1, 1
            # acquire answers
            maxLength_L, lenIn_L, lenDe_L = dfs(node.left)
            maxLength_R, lenIn_R, lenDe_R = dfs(node.right)
            # combine answers
            ## updata lenIn
            lenIn = 1
            if node.left is not None:
                if node.left.val + 1 == node.val:
                    lenIn = max([lenIn, lenIn_L + 1])
            if node.right is not None:
                if node.right.val + 1 == node.val:
                    lenIn = max([lenIn, lenIn_R + 1])
            ## update lenDe
            lenDe = 1
            if node.left is not None:
                if node.left.val - 1 == node.val:
                    lenDe = max([lenDe, lenDe_L + 1])
            if node.right is not None:
                if node.right.val - 1 == node.val:
                    lenDe = max([lenDe, lenDe_R + 1])
            ## update length
            ### length of a sequense that increase in left subtree 
            ### and decrease in right subtree
            length_Lin_Rde = 1
            if node.left is not None:
                if node.left.val + 1 == node.val:
                    length_Lin_Rde += lenIn_L
            if node.right is not None:
                if node.right.val - 1 == node.val:
                    length_Lin_Rde += lenDe_R
            ### length of a sequense that decrease in left subtree 
            ### and increase in right subtree
            length_Lde_Rin = 1
            if node.left is not None:
                if node.left.val - 1 == node.val:
                    length_Lde_Rin += lenDe_L
            if node.right is not None:
                if node.right.val + 1 == node.val:
                    length_Lde_Rin += lenIn_R
            ## update maxLength
            maxLength = max([maxLength_L,
                             maxLength_R,
                             length_Lin_Rde,
                             length_Lde_Rin])
            # return combined answer
            return maxLength, lenIn, lenDe
        return dfs(root)[0]
```

special care:
- 无论左右是否存在，都先准备好答案，如果存在，就依照存在的子树update答案
- 善用max()来update答案
- 少用if-else多用if，使判断为二元判断而不是多元判断
- 每一个返回值用一段独立的代码进行combine，从原材料开始combine，最后update真返回值