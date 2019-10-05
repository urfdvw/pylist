# Binary Tree

## 模板和要点
binary tree DC 模板
```python
def dfs(node):
    # if no such a node
    if node is None:
        # 目的一，default for empty tree
        # 目的二，增广二叉树边缘的 None。【依此思考】
    # if leaf
    if node.left is None and node.right is None:
        # 递归逻辑的真正出口
        # 只有leaf的树的返回值。【依此思考】
    # acquire answers
    # conbine answers
    # return conbined answer
    return Ans

return dfs(root)  # dfs(root)[0]
```
要点
- 遍历的是增广二叉树而不是二叉树本身，就是说所有的None都曾作为函数输入
- Divide conquer, is recusion
    - 递归函数的定义
    - 递归的body
    - 出口
- 然而返回条件有两种
    - 遇到叶节点
    - 遇到增广二叉树的边缘None

## Examples
- [97. Maximum Depth of Binary Tree](lint97.md)
- [480. Binary Tree Paths](lint480.md)
- [596. Minimum Subtree](lint596.md)
- [93](lint93.md)
- [597](lint597.md)
- [453](lint453.md)
- [88](lint88.md)
- [595](lint595.md)
- [614](lint614.md)
- [95](lint95.md)
- 900
- 902
- 578
- 95
- 901
- 86

## MISC
- 二叉树定义
    - full：每个节点都有两个或者没有子节点
    - balanced：左右子树高度差不超过1
    - complete：先填满靠近root的层再去填下层，且每层从左往右填
- pre-, in-, postorder 都是 DFS
- dfs函数最好还是单独写一个函数
    - 原因一是因为返回值多的时候总是要单独写的，所以就统一单独写不多想了
    - 原因二还是方便处理可能的除了empty tree之外的corner case
    - 原因三是不用写self.什么的
- ```f(x)[0]```是只要第一个返回值的意思
- BST 的in-order是非递减序列，但in-order是非递减序列的二叉树不一定是BST。这要看BST把相等定义在了哪边。