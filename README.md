# Contents
- [Coding Style](note_style.md)
- [Breadth First Search](note_bfs.md)
- [Non-Algorithm Problems](note_non_alg.md)

# Binary search
## 0. Find target index: find any/first/last target in the list
```python
# corner cases
# init boundaries
while(low + 1 < up):
    # while up and low are not next to each other
    mid = int(low + (up - low)/2)
    if(nums[mid] == target):
    elif(nums[mid] > target):
    else:  # (nums[mid] < target)
# check wether up or low
# if not found
```
- 模板关键点
    - 相邻即退出
        - while(low + 1 < up):
    - mid = (low - up)/2 + low
    - 比较的三种情况==, >, <
        - 全部都是 = mid
        - 情况 ==
            - 如果求any position，可以返回
            - 如果求first，up = min
            - 剩下一种你猜
        - 情况 target < list[mid]
            - up = mid
        - 剩下一种你猜
    - 判断到底返回up还是low
        - 顺序可能有讲究
- ex: 
    [457](lint457.md),
    [14](lint14.md),
    [458](lint458.md),
    [447](lint447.md)

## 1. Binary search by condition: find any/first/last element in list that
- 要素：
    - list的前后两半分别满足与不满足**某个条件**
    - 找到满足和不满足**分界**的地方
- 注意
    - 判断只有两项，及满足or不满足
    - 返回时候不用check，因为up和low的propertie不变，所以可以知道该返回哪个。
    - 注意要返回的是index还是element，都有可能
- ex: 
    [74](lint74.md),
    [159](lint159.md)

## 2. 缩小有解范围的大小
- 要素：
    - 要寻找***any***解的位置
    - 可以通过两界的性质判区间内是否有解
- ex: 
    [75](lint75.md)

## 3. 按结果搜索
- 要素
    - 题目要求的函数是一个复杂过程，let's call it backward process
    - 但是其逆过程是一个简单过程，let's call it forward process
    - 题目要求的函数输入输出都是scaler，且是一个单调函数。
    - 目前猜测，这类问题都可以转换为binary search by condition问题
- ex: 
    [141](lint141.md),
    [183](lint183.md),
    [437](lint437.md)

## MISC
- 如果明确要求olog(n)，一定是二分法
- 除了明显是递归的题，能不递归就不递归
- ["bisect" package examples](bisect.md)

---
# Binary Tree
- 二叉树
    - full：每个节点都有两个或者没有子节点
    - balanced：左右子树高度差不超过1
    - complete：先填满靠近root的层再去填下层，且每层从左往右填
- binary tree DC 模板
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
- 模板关键点
    - 遍历的是增广二叉树而不是二叉树本身，就是说所有的None都曾作为函数输入
    - Divide conquer, is recusion
        - 递归函数的定义
        - 递归的body
        - 出口
    - 然而返回条件有两种
        - 遇到叶节点
        - 遇到增广二叉树的边缘None

- examples
[97](lint97.md),
[480](lint480.md),
[596](lint596.md),
[93](lint93.md),
[597](lint597.md),
[453](lint453.md),
[88](lint88.md),
[595](lint595.md),
[614](lint614.md),
[95](lint95.md),

## MISC
- pre-, in-, postorder 都是 DFS
- dfs函数最好还是单独写一个函数
    - 原因一是因为返回值多的时候总是要单独写的，所以就统一单独写不多想了
    - 原因二还是方便处理可能的除了empty tree之外的corner case
    - 原因三是不用写self.什么的
- ```f(x)[0]```是只要第一个返回值的意思
- BST 的in-order是非递减序列，但in-order是非递减序列的二叉树不一定是BST。这要看BST把相等定义在了哪边。

