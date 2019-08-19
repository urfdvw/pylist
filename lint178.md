# [178. Graph Valid Tree](https://www.lintcode.com/problem/graph-valid-tree/description)

Given n nodes labeled from 0 to n - 1 and a list of undirected edges (each edge is a pair of nodes), write a function to check whether these edges make up a valid tree.

You can assume that no duplicate edges will appear in edges. Since all edges are undirected, [0, 1] is the same as [1, 0] and thus will not appear together in edges.

Example 1:
```
Input: n = 5 edges = [[0, 1], [0, 2], [0, 3], [1, 4]]
Output: true.
```
Example 2:
```
Input: n = 5 edges = [[0, 1], [1, 2], [2, 3], [1, 3], [1, 4]]
Output: false.
```
## Solution
```python
class Solution:
    """
    @param n: An integer
    @param edges: a list of undirected edges
    @return: true if it's a valid tree, or false
    """
    def validTree(self, n, edges):
        # corner case
        ## empty graph
        if len(edges) == 0:
            if n == 1:
                return True
            else:
                return False
        # test number of edges
        if n != len(edges) + 1:
            return False
        # test fully connected
        ## build graph
        graph = dict()
        ### build nodes
        for e in edges:
            graph[e[0]] = set()
            graph[e[1]] = set()
        ### build edges
        for e in edges:
            graph[e[0]].add(e[1])
            graph[e[1]].add(e[0])
        ## init bsf by putting 0 in queue
        if 0 not in graph:
            # if 0 not connected to any node, not fully connected
            return False
        queue = collections.deque([0])
        queued = {0}
        ## BFS loop
        while queue:
            # current node
            node = queue.popleft()
            # add next level nodes if never queued
            for nei in graph[node]:
                if nei not in queued:
                    queue.append(nei)
                    queued.add(nei)
        if len(queued) != n:  # if didn't queued all nodes
            return False
        return True
```
queued记录访问与否的set应当作为是否可以放入queue的提前审查。所以其动作应当与queue同步。

special care
- 图是树的条件
    - 边数等于节点数-1
    - 全连通（BFS来求）
- empty graph is corner case, because BSF must start from a node, but empty dose not have a node to start form.
- when building a graph, first node then edge

[Breadth First Search](2bfs.md)