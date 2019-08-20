# [616. Course Schedule II](https://www.lintcode.com/problem/course-schedule-ii/description)

There are a total of n courses you have to take, labeled from 0 to n - 1.
Some courses may have prerequisites, for example to take course 0 you have to first take course 1, which is expressed as a pair: [0,1]

Given the total number of courses and a list of prerequisite pairs, return the ordering of courses you should take to finish all courses.

There may be multiple correct orders, you just need to return one of them. If it is impossible to finish all courses, return an empty array.

Example 1:
```
Input: n = 2, prerequisites = [[1,0]] 
Output: [0,1]
```
Example 2:
```
Input: n = 4, prerequisites = [[1,0],[2,0],[3,1],[3,2]] 
Output: [0,1,2,3] or [0,2,1,3]
```
# Solution
```python
class Solution:
    """
    @param: numCourses: a total of n courses
    @param: prerequisites: a list of prerequisite pairs
    @return: the course order
    """
    def findOrder(self, numCourses, prerequisites):
        # build a graph 
        ## build a dictionary of list
        ## pre[1] -> pre[0]
        graph = dict()
        indregree = [0] * numCourses
        ## build nodes
        for n in range(numCourses):
            graph[n] = []
        ## build edges
        for pre in prerequisites:
            graph[pre[1]].append(pre[0]) 
            indregree[pre[0]] += 1
        # topology sorting
        order_of_taking = []
        queue = collections.deque()
        for n in range(numCourses):
            if indregree[n] == 0:
                queue.append(n)
        while queue:
            node = queue.popleft()
            for nei in graph[node]:
                indregree[nei] -= 1
                if indregree[nei] == 0:
                    queue.append(nei)
            order_of_taking.append(node)
        if len(order_of_taking) == numCourses:
            return order_of_taking
        else:
            return []
```
Special care:
- return [] when not DAG