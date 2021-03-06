# Binary Tree

## 模板和要点
binary tree DC 模板
```python
def dfs(node, size):
    # if no such a node
    if node is None:
        # 目的一，default for empty tree
        # 目的二，增广二叉树边缘的 None。【依此思考】
    # if leaf
    if node.left is None and node.right is None:
        # 递归逻辑的真正出口
        # 只有leaf的树的返回值。【依此思考】
    # acquire answers
    left_ans = dfs(node.left, size-1)
    right...
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
- ans一般不止一个，相互之间是依赖关系
    - 比如返回dfs(root)[0]的话，一定是[0]的计算依靠[1],[1]的计算依靠[2]，以此类推。

非递归的模板。非递归的DFS是用有限状态机来实现的。二叉树的话一共有4种状态。无论是pre/in/post-order，逻辑是完全一样的，只有顺序差别。
[详情请看这个notebook](misc/fsa_dsf.ipynb)

## Examples

- Binary Tree
    - [97. Maximum Depth of Binary Tree](lint97.md)
    - [596. Minimum Subtree](lint596.md)
    - [597. Subtree with Maximum Average](lint597.md)
    - [480. Binary Tree Paths](lint480.md)
    - [453. Flatten Binary Tree to Linked List](lint453.md)
    - [93. Balanced Binary Tree](lint93.md)
    - [88. Lowest Common Ancestor of a Binary Tree](lint88.md)
    - [578. Lowest Common Ancestor III](lint578.md)
    - [595. Binary Tree Longest Consecutive Sequence](lint595.md)
    - [614. Binary Tree Longest Consecutive Sequence II](lint614.md)
    - [543. Diameter of Binary Tree](leet543.md)
    - [124. Binary Tree Maximum Path Sum](leet124.md)
    - [404. Sum of Left Leaves](leet404.md)
    - [1026. Maximum Difference Between Node and Ancestor](leet1026.md)
- Binary Search Tree
    - [900. Closest Binary Search Tree Value](lint900.md)
    - [902. Kth Smallest Element in a BST](lint902.md)
    - [95. Validate Binary Search Tree](lint95.md)
    - [1008. Construct Binary Search Tree from Preorder Traversal](leet1008.md)
- non-recursion
    - [86. Binary Search Tree Iterator](lint86.md)
    - 901
- traverse
    - [Check If a String Is a Valid Sequence from Root to Leaves Path in a Binary Tree](leetw5.md)


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