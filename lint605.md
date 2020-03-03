# [605. Sequence Reconstruction](https://www.lintcode.com/problem/sequence-reconstruction/description)
Check whether the original sequence org can be uniquely reconstructed from the sequences in seqs. The org sequence is a permutation of the integers from 1 to n, with 1 ≤ n ≤ 10^4. Reconstruction means building a shortest common supersequence of the sequences in seqs (i.e., a shortest sequence so that all sequences in seqs are subsequences of it). Determine whether there is only one sequence that can be reconstructed from seqs and it is the org sequence.

Example 1:
```
Input:org = [1,2,3], seqs = [[1,2],[1,3]]
Output: false
Explanation:
[1,2,3] is not the only one sequence that can be reconstructed, because [1,3,2] is also a valid sequence that can be reconstructed.
```
Example 2:
```
Input: org = [1,2,3], seqs = [[1,2]]
Output: false
Explanation:
The reconstructed sequence can only be [1,2].
```
Example 3:
```
Input: org = [1,2,3], seqs = [[1,2],[1,3],[2,3]]
Output: true
Explanation:
The sequences [1,2], [1,3], and [2,3] can uniquely reconstruct the original sequence [1,2,3].
```
Example 4:
```
Input:org = [4,1,5,2,6,3], seqs = [[5,2,6,3],[4,1,5,2]]
Output:true
```

# Solution
```python
class Solution:
    """
    @param org: a permutation of the integers from 1 to n
    @param seqs: a list of sequences
    @return: true if it can be reconstructed only one or false
    """
    def sequenceReconstruction(self, org, seqs):
        """
            return true if
                seqs is DAG and have unique topological order
            and
                topological order is the same as org
        """
        # corner case
        ## the insane double empty case
        if len(org) == 0 and sum([len(s) for s in seqs]) == 0:
            return True
        # build graph from seq
        ## build nodes
        graph = dict()
        indegree = dict()
        for s in seqs:
            for n in s:
                graph[n] = []
                indegree[n] = 0
        ## build edges
        ### point from left to right
        for s in seqs:
            for i in range(len(s)-1):
                graph[s[i]].append(s[i+1])
                indegree[s[i+1]] += 1
        # topology sorting
        tp_sort = []
        queue = collections.deque()
        for node, degree in indegree.items():
            if degree == 0:
                queue.append(node)
        while queue:
            if len(queue) > 1:
                return False
            node = queue.popleft()
            tp_sort.append(node)
            for nei in graph[node]:
                indegree[nei] -= 1
                if indegree[nei] == 0:
                    queue.append(nei)
        # check if reconstructed right
        ## if same length
        if len(tp_sort) != len(org):
            return False
        ## if same numbers
        for i in range(len(org)):
            if org[i] != tp_sort[i]:
                return False
        return True
```
        
# Question to ask
- can i assume that the numbers are unique? Yes!
Special care:
- Need to check at the end
    - if the length are the same, other wise not DAG
    - if the reconstruction same as ```org```, otherwise return ```False```