# [102. Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal/)

Given the root of a binary tree, return the level order traversal of its nodes' values. (i.e., from left to right, level by level).

Example 1:

![](https://assets.leetcode.com/uploads/2021/02/19/tree1.jpg)

    Input: root = [3,9,20,null,null,15,7]
    Output: [[3],[9,20],[15,7]]

Example 2:

    Input: root = [1]
    Output: [[1]]

Example 3:

    Input: root = []
    Output: []
 

Constraints:
- The number of nodes in the tree is in the range [0, 2000].
- -1000 <= Node.val <= 1000

# Solution
[Code Steps](./presentations/?id=leet102)
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def levelOrder(self, root: Optional[TreeNode]) -> List[List[int]]:
        # corner case
        if root is None:
            return []
        # regular case (BFS)
        layers = [] # contains all layers
        q = deque([root]) # queue
        while q:
            current_layer = [] # contains node values
            for i in range(len(q)): # one layer
                # dequeue
                node = q.popleft()
                # process current layer
                current_layer.append(node.val)
                # append children if any
                if node.left is not None:
                    q.append(node.left)
                if node.right is not None:
                    q.append(node.right)
            layers.append(current_layer) # append current layer to answer
        return layers
```
```steps
1, 2, 3, 4, 5, 6, 7, 8
13
28
14
15
17
16
18
20
22
19
21
23
24
25, 26
27
12
9, 10
11
```

# Another solution 

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def levelOrder(self, root: Optional[TreeNode]) -> List[List[int]]:
        if root is None:
            return []
        
        q = deque([root])
        layers = []
        while q:
            layers.append([node.val for node in list(q)])
            for i in range(len(q)):
                node = q.popleft()
                if node.left is not None:
                    q.append(node.left)
                if node.right is not None:
                    q.append(node.right)
        return layers

```
Note:
- `bool([None])` is still `True`, because the lenth of the list is `1`
- beacuse of the `for` loop, each `while` loop iterate through a layer, thus `layers.append([node.val for node in list(q)])` makes sense.