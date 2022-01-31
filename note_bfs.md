# Breadth First Search

## 模板和要點

基本模板：BFS on tree

``` python
# Init
q = deque([root]) # 用作 queue
# loop
while q: # 当 q 不为空
    node = q.popleft() # 当前节点
    # 对当前节点进行操作
    # 遍历子节点：
        # append 到 q
```

要点
- 节点的主逻辑紧接在 ```popleft()``` 之后

---

基本模板的变体

``` python
# Init
## 处理 root
q = deque([root]) # 用作 queue
# loop
while q: # 当 q 不为空
    node = q.popleft() # 当前节点
    # 遍历子节点：
        # 对当前子节点进行操作
        # append 到 q
```

要点
- 对 node 的处理是紧贴 append 之前

---

进阶 1，分层遍历

``` python
# Init
q = deque([root]) # 用作 queue
layer = 0 #!! 当前层 index
# loop
while q: # 当 q 不为空
    for _ in range(len(q)): #!! index `_` 不重要
        node = q.popleft() # 当前节点
        # 对当前节点进行操作
        # 遍历子节点：
            # append 到 q
    layer += 1 #!! 层 index 加一
```

要点
- 每一个 ```for``` 循环(all iterations) 都是完整的一层
- 每运行完一个```for``` 循环(all iterations) q 里面存着下一层的全部节点

---

进阶 2，图上的 BFS，加入查重

``` python
# Init
q = deque([root]) # 用作 queue
qed = set(q) #!! 用于记录进入过 q 的节点
layer = 0 # 当前层 index
# loop
while q: # 当 q 不为空
    for _ in range(len(q)): # index `_` 不重要
        node = q.popleft() # 当前节点
        # 对当前节点进行操作
        # 遍历子节点：
            if 子节点 not in qed: #!! 之前是否进入过 q
                # append 到 q
                #!! add 到 qed
    layer += 1 # 层 index 加一
```

要点
- qed 只记录 **“进入 q”** 这个动作，来避免重复
    - q 一变 qed 一定要同步变化
    
<!-- - 如果所有的nei node已经定义好了，可以考虑qed.add(对象)；如果没有，必须用qed.add(label)
    - 隐式图中，因为所有neighbor都是新生成的元素，所以要qed.add(label)。
    - 如果不想想的话，q里面放对象，qd里面放label。
- 图在python里的简便实现：dict of list -->

---
进阶 3， Topology sorting

``` python
# 定义
graph = dict() #!! key: node label, value [label of neighbors dicts]
indegree = dict() #!! key: node label, value int indegree
# 初始化
q = deque([]) #!! 中包含所有indegree == 0 的 node
# BFS loop
while q: # 当 q 不为空
    node = q.popleft() # 当前节点
    # 对当前节点进行操作, 记述或者记录
    # 遍历子节点 nei：
        indegree[nei] -= 1 #!! 入度减一
        if indegree[nei] == 0: #!! 如果入度已经减为零
            q.append(nei) # append 到 q
```

要点
- 不需要qd因为有indegree
- 能够遍历全部全部的节点 说明可 topology sort
- 一直保持 len(q) <= 1 说明可唯一 topology sort

## Examples
- On Tree
    - [69. Binary Tree Level Order Traversal](lint69.md)
        - [102. Binary Tree Level Order Traversal](leet102.md)
    - [7. Serialize and Deserialize Binary Tree](lint7.md)
        - [297. Serialize and Deserialize Binary Tree](leet297.md)
- On Graph
    - [178. Graph Valid Tree](lint178.md)
        - [261. Graph Valid Tree](leet261.md)
    - [137. Clone Graph](lint137.md)
        - [133. Clone Graph](leet133.md)
- On Implicit Graph
    - [433. Number of Islands](lint433.md)
        - [200. Number of Islands](leet200.md)
    - [611. Knight Shortest Path](lint611.md)
    - [1197. Minimum Knight Moves](leet1197.md)
    - [120. Word Ladder](lint120.md)
        - [127. Word Ladder](leet127.md)
- topology sorting
    - [615. Course Schedule](lint615.md)
    - [616. Course Schedule II](lint616.md)
    - [605. Sequence Reconstruction](lint605.md)
    - [127. Topological Sorting](lint127.md)

## MISC
- python 里面的 collections.deque() 可以用作 queue
    - enqueue: a.append()
    - dequeue: a.popleft()
<!-- - a.append(), a.pop() 可以当作stack的接口用
- set 的函数
    - A.add()
    - A.remove()
    - X in A
- dict 的函数
    - X in B  # 测试 X 是否是 B 的 key -->
- 需要遍历的时候，优先考虑BFS。
    - 比如序列化
- 最短路几乎全是 BFS