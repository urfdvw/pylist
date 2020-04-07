# [107. Word Break](https://www.lintcode.com/problem/word-break/description)

Given a string s and a dictionary of words dict, determine if s can be broken into a space-separated sequence of one or more dictionary words.

Example 1:
```
	Input:  "lintcode", ["lint", "code"]
	Output:  true
```
Example 2:
```
	Input: "a", ["a"]
	Output:  true
```

# Solution
```python
from functools import lru_cache
class Solution:
    """
    @param: s: A string
    @param: dic: A set of words dict
    @return: A boolean
    """
    def wordBreak(self, s, dic):
        # nonsense
        if len(s) == 0:
            return True
        self.dic = dic
        return self.dfs(s)
        
    @lru_cache(None)
    def dfs(self, s):
        if s in self.dic:
            return True
        for i in range(1, len(s)+1):
            if s[0:i] in self.dic:
                return self.dfs(s[i:])
        return False
```

# care
- a helper function is necessary because dic should not be considered as a input for a lru_cache() function.