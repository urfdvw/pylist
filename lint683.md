# [683. Word Break III](https://www.lintcode.com/problem/word-break-iii/description)

Give a dictionary of words and a sentence with all whitespace removed, return the number of sentences you can form by inserting whitespaces to the sentence so that each word can be found in the dictionary.

Example 1
```
Input:
"CatMat"
["Cat", "Mat", "Ca", "tM", "at", "C", "Dog", "og", "Do"]
Output: 3
Explanation:
we can form 3 sentences, as follows:
"CatMat" = "Cat" + "Mat"
"CatMat" = "Ca" + "tM" + "at"
"CatMat" = "C" + "at" + "Mat"
```
Example1
```
Input:
"a"
[]
Output: 0
```
Notice: Ignore case

# Solution
```python
from functools import lru_cache
class Solution:
    """
    @param: s: A string
    @param: dic: A set of words dict
    @return: A boolean
    """
    def wordBreak3(self, s, dic):
        # nonsense
        if len(s) == 0:
            return 1
        self.dic = set([d.lower() for d in dic if len(d) > 0])
        return self.dfs(s.lower())
        
    @lru_cache(None)
    def dfs(self, s):
        ans = 0
        
        if s in self.dic:
            ans += 1
        
        for i in range(1, len(s)+1):
            if s[0:i] in self.dic:
                ans += self.dfs(s[i:])
                
        return ans
```

# care
- the dic might contain non-sense empty string