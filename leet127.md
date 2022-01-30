# [127. Word Ladder](https://leetcode.com/problems/word-ladder/)
A transformation sequence from word beginWord to word endWord using a dictionary wordList is a sequence of words beginWord -> s1 -> s2 -> ... -> sk such that:

Every adjacent pair of words differs by a single letter.
Every si for 1 <= i <= k is in wordList. Note that beginWord does not need to be in wordList.
sk == endWord
Given two words, beginWord and endWord, and a dictionary wordList, return the number of words in the shortest transformation sequence from beginWord to endWord, or 0 if no such sequence exists.

Example 1:

    Input: beginWord = "hit", endWord = "cog", wordList = ["hot","dot","dog","lot","log","cog"]
    Output: 5
    Explanation: One shortest transformation sequence is "hit" -> "hot" -> "dot" -> "dog" -> cog", which is 5 words long.

Example 2:

    Input: beginWord = "hit", endWord = "cog", wordList = ["hot","dot","dog","lot","log"]
    Output: 0
    Explanation: The endWord "cog" is not in wordList, therefore there is no valid transformation sequence.

Constraints:

- 1 <= beginWord.length <= 10
- endWord.length == beginWord.length
- 1 <= wordList.length <= 5000
- wordList[i].length == beginWord.length
- beginWord, endWord, and wordList[i] consist of lowercase English letters.
- beginWord != endWord
- All the words in wordList are unique.

# Solution
[Code Steps](./presentations/?id=leet127)
```python
class Solution:
    def ladderLength(self, begin: str, end: str, word_list: List[str]) -> int:
        # change list to set
        word_set = set(word_list)
        # BFS
        q = deque([begin])
        qed = set(q)
        layer = 1 # at least there is a beginning word
        while q:
            for i in range(len(q)):
                # pop
                word = q.popleft()
                # if found
                if word == end:
                    return layer
                # append nei
                for nei in self.find_nei(word, word_set):
                    if nei not in qed:
                        q.append(nei)
                        qed.add(nei)
            layer += 1
        # if did not found
        return 0
    
    def find_nei(self, word, word_set):
        """
        return [
            word[:i] + c + word[i+1:]
            for i in range(len(word))
            for c in 'qwertyuiopasdfghjklzxcvbnm'
            if word[:i] + c + word[i+1:] in word_set
        ]
        """
        return [
            new_word
            for i in range(len(word))
            for c in 'qwertyuiopasdfghjklzxcvbnm'
            if (new_word := word[:i] + c + word[i+1:]) in word_set
        ]
```
```steps
1,2
3,4
5
6
7
8
9
10
21
11,12
13
14
15
22,23
16,17,18,19,20
25
27,32
29
30
28
31
26,33
34,36,37,39
38
35
```
- `:=` 用于 list comprehension 非常合适
- `:=` 也可以用于复合条件
    - 下面的例子是：平方是奇数且平方小于100，注意 `sq` 的定义
```python
for i in range(20):
    if ((sq := i * i) % 2 == 1
        and sq < 100):
        print(i)
```