# [615. Course Schedule](https://www.lintcode.com/problem/course-schedule/description?_from=ladder&&fromId=1)

There are a total of n courses you have to take, labeled from 0 to n - 1.

Some courses may have prerequisites, for example to take course 0 you have to first take course 1, which is expressed as a pair: [0,1]

Given the total number of courses and a list of prerequisite pairs, is it possible for you to finish all courses?

Example 1:
```
Input: n = 2, prerequisites = [[1,0]] 
Output: true
```
Example 2:
```
Input: n = 2, prerequisites = [[1,0],[0,1]] 
Output: false
```
# Solution
```python
class Solution:
    """
    @param: numCourses: a total of n courses
    @param: prerequisites: a list of prerequisite pairs
    @return: true if can finish all courses or false
    """
    def canFinish(self, numCourses, prerequisites):
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
        n_of_course_taken = 0
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
            n_of_course_taken += 1
        # check if all courses are taken
        if n_of_course_taken == numCourses:
            return True
        else:
            return False
```
Special care:
- when building a graph, build nodes and then edges in seperate loops.
- 這裏取了個巧，因爲提供了numCourses而且課程的label是0~n-1，説以乾脆用list作爲indegree