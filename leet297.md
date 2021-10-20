# [297. Serialize and Deserialize Binary Tree](https://leetcode.com/problems/serialize-and-deserialize-binary-tree/)

Serialization is the process of converting a data structure or object into a sequence of bits so that it can be stored in a file or memory buffer, or transmitted across a network connection link to be reconstructed later in the same or another computer environment.

Design an algorithm to serialize and deserialize a binary tree. There is no restriction on how your serialization/deserialization algorithm should work. You just need to ensure that a binary tree can be serialized to a string and this string can be deserialized to the original tree structure.

Clarification: The input/output format is the same as how LeetCode serializes a binary tree. You do not necessarily need to follow this format, so please be creative and come up with different approaches yourself.

Example 1:

![](https://assets.leetcode.com/uploads/2020/09/15/serdeser.jpg)

    Input: root = [1,2,3,null,null,4,5]
    Output: [1,2,3,null,null,4,5]

Example 2:

    Input: root = []
    Output: []

Example 3:

    Input: root = [1]
    Output: [1]

Example 4:

    Input: root = [1,2]
    Output: [1,2]
 

Constraints:
- The number of nodes in the tree is in the range [0, 104].
- -1000 <= Node.val <= 1000

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Codec:
    def serialize(self, root):
        """Encodes a tree to a single string.
        
        :type root: TreeNode
        :rtype: str
        """
        if root is None:
            return ""
        
        out = [str(root.val)]
        q = deque([root])
        while q:
            node = q.popleft()
            for attr in ['left', 'right']:
                if getattr(node, attr) is None:
                    out.append('*')
                else:
                    out.append(str(getattr(node, attr).val))
                    q.append(getattr(node, attr))
                    
        return ','.join(out)
        
    def deserialize(self, data):
        """Decodes your encoded data to tree.
        
        :type data: str
        :rtype: TreeNode
        """
        if data == "":
            return None
        
        data = data.split(',')        
        root = TreeNode(int(data[0]))
        i = 1
        q = deque([root])
        while q:
            node = q.popleft()
            for attr in ['left', 'right']:
                if data[i] != '*':
                    setattr(node, attr, TreeNode(int(data[i])))
                    q.append(getattr(node, attr))
                i += 1
                    
        return root

# Your Codec object will be instantiated and called as such:
# ser = Codec()
# deser = Codec()
# ans = deser.deserialize(ser.serialize(root))
```
- 这个答案优雅的地方在于，解码和编码的结构完全一样
- decoder 里，之所以 `data = [int(d) for d in data.split(',')]` 不行，是因为中间有`*`
    - 另外说，int 没有 inf 的值，只有 float 有
- `getattr` 和 `setattr` 不是成员函数，而是 built-in
- decoder 也可以用 deque 就可以省去记录一个 index
```python
def deserialize(self, data):
    """Decodes your encoded data to tree.
    
    :type data: str
    :rtype: TreeNode
    """
    if data == "":
        return None
    
    data = deque(data.split(','))
    root = TreeNode(int(data.popleft()))
    q = deque([root])
    while q:
        node = q.popleft()
        for attr in ['left', 'right']:
            val = data.popleft()
            if val != '*':
                setattr(node, attr, TreeNode(int(val)))
                q.append(getattr(node, attr))
                
    return root
```