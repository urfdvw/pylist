# Breadth First Search

## 模板
- On Tree
    -   ```
        # 初始化
        queue = deque() 中有且仅有如根节点一个元素
        layer = 0 (试layer的定义可能有变)
        # BFS loop
        while queue:
            for _ in range(len(queue)) (层级遍历)
                node = queue.popleft()
                对当前节点进行主逻辑
                如果有儿子，就加入队列
            layer += 1
        ```
    - 要点
        - 某一层遍历完之后，queue中的元素是下一层的全部元素。

- On Graph
    -   ```
        # 初始化
        queue = deque() 中包含所有可能的开始点
        queued = set(queue)
        layer = 0 (试layer的定义可能有变)
        # BFS loop
        while queue:
            for _ in range(len(queue)) (层级遍历)
                node = popleft()
                对当前节点进行主逻辑
                for nei in 所有邻居:
                    if nei not in queued:
                        queue.append(nei)
                        queued.add(nei)
            layer += 1
        ```
    - 要点
        - 要记录queued node以避免重复enqueue
            - queue 一变 queued一定要同步变化
        - 如果所有的nei node已经定义好了，可以考虑queued.add(对象)；如果没有，必须用queued.add(label)。
            - 隐式图中，因为所有neighbor都是新生成的元素，所以要queued.add(label)。
            - 如果不想想的话，queue里面放对象，queued里面放label。
        - 图在python里的简便实现：map of list
        
- Topology sorting
    -   ```
        # 定义
        图 dict(), key: node label, value [label of neighbors]
        indegree, key: node label, value int indegree
        # 初始化
        queue = deque() 中包含所有indegree == 0 的 node
        tpsort = []
        layer = 0 (试layer的定义可能有变)
        # BFS loop
        while queue:
            for _ in range(len(queue)) (层级遍历)
                node = popleft()
                tpsort.append(node)
                for nei in 所有邻居:
                    indegree[nei] -= 1
                    if indegree[nei] == 0:
                        queue.append(nei)
            layer += 1
        ```
    - 要点
        - 不需要queued因为有indegree
        - len(tpsort) == len(indegree) 说明可 topology sort
        - 一直保持 len(queue) <= 1 说明可唯一 topology sort

## Examples
- On Tree
    - [69. Binary Tree Level Order Traversal](lint69.md)
    - [7. Serialize and Deserialize Binary Tree](lint7.md)
- On Graph
    - [178. Graph Valid Tree](lint178.md)
    - [137. Clone Graph](lint137.md)
- On hidden Graph
    - [433. Number of Islands](lint433.md)
- topology sorting
    - [615. Course Schedule](lint615.md)
    - [616. Course Schedule II](lint616.md)

## MISC
- python 里面的 collections.deque()
    - enqueue: a.append()
    - dequeue: a.popleft()
- a.append(), a.pop() 可以当作stack的接口用
- set 的函数
    - A.add()
    - A.remove()
    - X in A
- dict 的函数
    - X in B  # 测试X是否是B的key
- 需要遍历的时候，优先考虑BFS。
    - 比如序列化