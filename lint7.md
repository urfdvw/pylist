# [7. Serialize and Deserialize Binary Tree](https://www.lintcode.com/problem/serialize-and-deserialize-binary-tree/description)
Design an algorithm and write code to serialize and deserialize a binary tree. Writing the tree to a file is called 'serialization' and reading back from the file to reconstruct the exact same binary tree is 'deserialization'.

There is no limit of how you deserialize or serialize a binary tree, LintCode will take your output of serialize as the input of deserialize, it won't check the result of serialize.

Example 1:
```
Input：{3,9,20,#,#,15,7}
Output：{3,9,20,#,#,15,7}
Explanation：
Binary tree {3,9,20,#,#,15,7},  denote the following structure:
	  3
	 / \
	9  20
	  /  \
	 15   7
it will be serialized {3,9,20,#,#,15,7}
```
Example 2:
```
Input：{1,2,3}
Output：{1,2,3}
Explanation：
Binary tree {1,2,3},  denote the following structure:
   1
  / \
 2   3
it will be serialized {1,2,3}
```
Our data serialization use BFS traversal. This is just for when you got Wrong Answer and want to debug the input.

You can use other method to do serializaiton and deserialization.

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
    @param root: An object of TreeNode, denote the root of the binary tree.
    This method will be invoked first, you should design your own algorithm 
    to serialize a binary tree which denote by a root node to a string which
    can be easily deserialized by your own "deserialize" method later.
    """
    def serialize(self, root):
        # corner case
        ## empty tree
        if root is None:
            return '{}'
        # init: queue with root
        queue = collections.deque()
        queue.append(root)
        strlist = []
        # BFS loop
        while queue:
            node = queue.popleft()
            if node is None:  # if no such node
                strlist.append('#')
            else:  # if node exists
                # append child no matter its existence
                queue.append(node.left)
                queue.append(node.right)
                # record the value
                strlist.append(str(node.val))
        # cut the tailing '#'
        while strlist[-1] == '#':
            strlist.pop()
        # form the string from list
        return '{' + ','.join(strlist) + '}'
    """
    @param data: A string serialized by your serialize method.
    This method will be invoked second, the argument data is what exactly
    you serialized at method "serialize", that means the data is not given by
    system, it's given by your own serialize method. So the format of data is
    designed by yourself, and deserialize it here as you serialize it in 
    "serialize" method.
    """
    def deserialize(self, data):
        # corner case
        ## empty tree
        if data == '{}':
            return None
        # str data to list
        strlist = collections.deque(data[1: -1].split(','))
        # init: build a root in a queue
        root = TreeNode(strlist.popleft())
        queue = collections.deque()
        queue.append(root)
        # BFS loop
        while queue:
            node = queue.popleft()
            for child in ["left", "right"]:
                if strlist:  # might catched the end
                    val =  strlist.popleft()
                    if val == '#':
                        setattr(node, child, None)
                    else:
                        setattr(node, child, TreeNode(int(val)))
                        queue.append(getattr(node, child))
        return root
```
questions to ask:
- are the type of node.val int? Yes!

special care:
- When convert the string back to tree, need to use construction function of TreeNode class

[Breadth First Search](2bfs.md)

## Archived Solution
Problem with this solution
- code duplication in ```deserialize()```
- list as queue


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
    @param root: An object of TreeNode, denote the root of the binary tree.
    This method will be invoked first, you should design your own algorithm 
    to serialize a binary tree which denote by a root node to a string which
    can be easily deserialized by your own "deserialize" method later.
    """
    def serialize(self, root):
        # corner case
        ## empty tree
        if root is None:
            return '{}'
        # init: queue with root
        queue = [root]
        strlist = []
        # BFS loop
        while queue:
            node = queue.pop(0)
            if node is None:  # if no such node
                strlist.append('#')
            else:  # if node exists
                # append child no matter its existence
                queue.append(node.left)
                queue.append(node.right)
                # record the value
                strlist.append(str(node.val))
        # cut the tailing '#'
        while strlist[-1] == '#':
            strlist.pop()
        # form the string from list
        return '{' + ','.join(strlist) + '}'
    """
    @param data: A string serialized by your serialize method.
    This method will be invoked second, the argument data is what exactly
    you serialized at method "serialize", that means the data is not given by
    system, it's given by your own serialize method. So the format of data is
    designed by yourself, and deserialize it here as you serialize it in 
    "serialize" method.
    """
    def deserialize(self, data):
        # corner case
        ## empty tree
        if data == '{}':
            return None
        # str data to list
        strlist = data[1: -1].split(',')
        # init: build a root in a queue
        root = TreeNode(strlist.pop(0))
        queue = [root]
        # BFS loop
        while queue:
            node = queue.pop(0)
            if strlist:  # might catched the end
                valLeft =  strlist.pop(0)
                if valLeft == '#':
                    node.left = None
                else:
                    node.left = TreeNode(int(valLeft))
                    queue.append(node.left)
            if strlist:  # might catched the end
                valRight =  strlist.pop(0)
                if valRight == '#':
                    node.right = None
                else:
                    node.right = TreeNode(int(valRight))
                    queue.append(node.right)
        return root
```