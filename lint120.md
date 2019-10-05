# [120. Word Ladder](https://www.lintcode.com/problem/word-ladder/description?_from=ladder&&fromId=1)

Given two words (start and end), and a dictionary, find the shortest transformation sequence from start to end, output the length of the sequence.
Transformation rule such that:
- Only one letter can be changed at a time
- Each intermediate word must exist in the dictionary. (Start and end words do not need to appear in the dictionary )

info
- Return 0 if there is no such transformation sequence.
- All words have the same length.
- All words contain only lowercase alphabetic characters.
- You may assume no duplicates in the word list.
- You may assume beginWord and endWord are non-empty and are not the same.

Example 1:
```
Input：start = "a"，end = "c"，dict =["a","b","c"]
Output：2
Explanation：
"a"->"c"
```
Example 2:
```
Input：start ="hit"，end = "cog"，dict =["hot","dot","dog","lot","log"]
Output：5
Explanation：
"hit"->"hot"->"dot"->"dog"->"cog"
```
## Solution
```python
class Solution:
    def ladderLength(self, start, end, voc):
        """ BFS by layers of the words
        if end_word is found then return the layer number
        neighbors are words that differs by one letter
        
        in:
            start: a string
            end: a string
            voc: a set of string
        out:
            return: An integer
        """
        # add end into voc in case it is not there
        voc.add(end)
        # BFS by layer to search end
        queue = deque([start])
        queued = set(queue)
        layer = 1
        while queue:
            for _ in range(len(queue)):
                word = queue.popleft()
                if word == end:
                    return layer
                neighbors = self.get_neighbors(word, voc)
                for nei in neighbors:
                    if nei not in queued:
                        queue.append(nei)
                        queued.add(nei)
            layer += 1
        return 0
        
    def get_neighbors(self, word, voc):
        """ find words that differ from the word by 1 letter
        
        in:
            word: str:
        out:
            neighbors: list of str:
        """
        neighbors = []
        alpha = "abcdefghijklmnopqrstuvwxyz"
        for i_word in range(len(word)):
            for i_alpha in range(len(alpha)):
                if word[i_word] != alpha[i_alpha]:
                    new_word = word[0:i_word] + alpha[i_alpha] + word[i_word+1:]
                    if new_word in voc:
                        neighbors.append(new_word)
        return neighbors
```

Special care:
```start``` and ```end``` might not in the voc. This corner case is so stupid.