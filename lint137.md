# [137. Clone Graph](https://www.lintcode.com/problem/clone-graph/description)

Clone an undirected graph. Each node in the graph contains a label and a list of its neighbors. Nodes are labeled uniquely.

You need to return a deep copied graph, which has the same structure as the original graph, and any changes to the new graph will not have any effect on the original graph.

You need return the node with the same label as the input node.

[How we serialize an undirected graph](http://www.lintcode.com/help/graph/)

Example1
```
Input:
{1,2,4#2,1,4#4,1,2}
Output: 
{1,2,4#2,1,4#4,1,2}
Explanation:
1----2  
 \   |  
  \  |  
   \ |  
    \|  
     4   
```

## Solution
```python
"""
Definition for a undirected graph node
class UndirectedGraphNode:
    def __init__(self, x):
        self.label = x
        self.neighbors = []
"""


class Solution:
    """
    @param: node: A undirected graph node
    @return: A undirected graph node
    """
    def cloneGraph(self, node):
        # corner case
        ## insane empty graph
        if node is None:
            return None
            
        # bfs traverse function
        def bfs(node):
            """
            in: node: a node in the graph
            out: list of nodes: all nodes in the graphe
            """
            ans = []
            # init bfs
            queue = collections.deque([node])
            queued = {node.label}
            # loop
            while queue:
                # current node
                current = queue.popleft()
                # append neighbor
                for nei in current.neighbors:
                    if nei.label not in queued:
                        queue.append(nei)
                        queued.add(nei.label)
                # service
                ans.append(current)
            return ans
            
        # get the list of all nodes
        oldNodes = bfs(node)
        # copy nodes
        newNodes = dict()
        for n in oldNodes:
            newNodes[n.label] = UndirectedGraphNode(n.label)
        # copy edges
        for n in oldNodes:
            for nei in n.neighbors:
                newNodes[n.label].neighbors.append(newNodes[nei.label])
        # return node
        return newNodes[node.label]
```
Questions to ask
- Can I assume that the graph is connected? Yes!
- Can I assume the graph to be non-empty? No!
- Are the labels unique? Yes!

Special care
- class graphnode is not hashable, so not able to store in set(). So store labels.
- BFS loops are independent from service code.

[Breadth First Search](2bfs.md)

---

## Archived Solution
Another solution put all service code in BFS, which is bad.

This takes less space, but more running time because of the check of existence of itme.
```python
"""
Definition for a undirected graph node
class UndirectedGraphNode:
    def __init__(self, x):
        self.label = x
        self.neighbors = []
"""


class Solution:
    """
    @param: node: A undirected graph node
    @return: A undirected graph node
    """
    def cloneGraph(self, node):
        # corner case
        ## insane empty graph
        if node is None:
            return None
        # init BFS
        queue = [node]
        queued = {node.label}
        # map from label to constructed node
        l2cn = {node.label: UndirectedGraphNode(node.label)}  
        # BFS loop
        while queue:
            ## get current node
            current = queue.pop(0)
            ## append neighbors
            for nei in current.neighbors:
                if nei.label not in queued:
                    queue.append(nei)
                    queued.add(nei.label)
            ## service
            for nei in current.neighbors:
                if nei.label in l2cn:
                    # if the neighbor is already constructed
                    l2cn[current.label].neighbors.append(l2cn[nei.label])
                else:
                    l2cn[nei.label] = UndirectedGraphNode(nei.label)
                    l2cn[current.label].neighbors.append(l2cn[nei.label])
        return l2cn[node.label]
```