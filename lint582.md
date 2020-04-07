# [582. Word Break II](https://www.lintcode.com/problem/word-break-ii)

Given a string s and a dictionary of words dict, add spaces in s to construct a sentence where each word is a valid dictionary word.

Return all such possible sentences.

Example 1:
```
Input："lintcode"，["de","ding","co","code","lint"]
Output：["lint code", "lint co de"]
Explanation：
insert a space is "lint code"，insert two spaces is "lint co de".
```
Example 2:
```
Input："a"，[]
Output：[]
Explanation：dict is null.
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
            return 1
        self.dic = set([d.lower() for d in dic if len(d) > 0])
        ans = self.dfs(s.lower())
        return [' '.join(a) for a in ans]
        
    @lru_cache(None)
    def dfs(self, s):
        ans = []
        
        if s in self.dic:
            ans.append([s])
        
        for i in range(1, len(s)+1):
            if s[0:i] in self.dic:
                cur_ans = self.dfs(s[i:])
                ans += [[s[0:i]] + c for c in cur_ans]
                
        return ans
        
```
# care
- the dic might contain non-sense empty string