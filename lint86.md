# [86. Binary Search Tree Iterator](https://www.lintcode.com/problem/binary-search-tree-iterator/)
Design an iterator over a binary search tree with the following rules:

Elements are visited in ascending order (i.e. an in-order traversal)

next() and hasNext() queries run in O(1) time in average.

Example 1
```
Input:  {10,1,11,#,6,#,12}
Output:  [1, 6, 10, 11, 12]
Explanation:
The BST is look like this:
  10
  /\
 1 11
  \  \
   6  12
You can return the inorder traversal of a BST [1, 6, 10, 11, 12]
```
Example 2
```
Input: {2,1,3}
Output: [1,2,3]
Explanation:
The BST is look like this:
  2
 / \
1   3
You can return the inorder traversal of a BST tree [1,2,3]
```
Challenge
```
Extra memory usage O(h), h is the height of the tree.

Super Star: Extra memory usage O(1)
```
# Solution
```python
"""
Definition of TreeNode:
class TreeNode:
    def __init__(self, val):
        self.val = val
        self.left, self.right = None, None

Example of iterate a tree:
iterator = BSTIterator(root)
while iterator.hasNext():
    node = iterator.next()
    do something for node 
"""

"""
state definination

in order 
  l - v - r
0 - 1 - 2 - 3
"""

class BSTIterator:
    """
    @param: root: The root of binary tree.
    """
    def __init__(self, root):
        self.stack = []
        self.n = root
        self.s = 0
        if root is None:
            self.pre = None
        else:
            self.pre = self.pre_next()
        return 
    
    """
    @return: True if there has next node, or false
    """
    def hasNext(self):
        if self.pre is None:
            return False
        else:
            return True
    """
    @return: return next node
    """
    def next(self):
        out = self.pre
        self.pre = self.pre_next()
        return out
    """
    test run of next function
    """
    def pre_next(self):
        while 1:
            if self.s == 0:
                if self.n.left is None:
                    self.s = 1
                    continue
                else:
                    self.stack.append((self.n, 1))
                    self.n = self.n.left
                    self.s = 0
                    continue
            if self.s == 1:
                self.s = 2
                return self.n
            if self.s == 2:
                if self.n.right is None:
                    self.s = 3
                    continue
                else:
                    self.stack.append((self.n, 3))
                    self.n = self.n.right
                    self.s = 0
                    continue
            if self.s == 3:
                if len(self.stack) == 0:
                    break
                else:
                    self.n, self.s = self.stack.pop()
                continue
            return None
```

# Special care
- 这个答案使用了[有限状态机的非递归DFS](misc/fsa_dfs.ipynb)。
- 如果不用上述算法尝试一下，很难知道有没有下一个输出，所以设置了一个pre_next函数，在调用之前一个周期就计算好结果。