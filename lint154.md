# [154. Regular Expression Matching](https://www.lintcode.com/problem/regular-expression-matching/description)

Implement regular expression matching with support for '.' and '*'.

- '.' Matches any single character.
- '*' Matches zero or more of the preceding element.
The matching should cover the entire input string (not partial).


The function prototype should be:

`bool isMatch(string s, string p)`

```
isMatch("aa","a") → false

isMatch("aa","aa") → true

isMatch("aaa","aa") → false

isMatch("aa", "a*") → true

isMatch("aa", ".*") → true

isMatch("ab", ".*") → true

isMatch("aab", "c*a*b") → true
```

Example 1:
```
Input："aa"，"a"
Output：false
Explanation：
unable to match
```
Example 2:
```
Input："aa"，"a*"
Output：true
Explanation：
'*' can repeat a
```

# Solutions
```python
from functools import lru_cache
class Solution:
    """
    @param s: A string 
    @param p: A string includes "." and "*"
    @return: A boolean
    """
    def isMatch(self, s, p):
        
        if len(p) > 0:
            if p[0] == '*':
                return False
                
        while not p.find('**') == -1:
            p = p.replace('**', '*', p.count('**'))
        
        return self.dp(s, p)
        
    @ lru_cache(None)
    def dp(self, s, p):
        if s == p:
            return True
            
        if len(p) == 0:
            return False
            
        if len(p) >= 2:
            if p[1] == '*':
                for i in range(len(s) + 1): # at most there should be a p = '.' * len(s)
                    if self.dp(s, p[0] * i + p[2:]):
                        return True
                return False
            
        if len(s) == 0:
            return False
        
        if p[0] == '.' or s[0] == p[0]:
            return self.dp(s[1:], p[1:])
            
        if s[0] != p[0]:
            return False
            
        return False
```
# care
- `*` 的意思是重复前面的符号。`isMatch("ab", ".*") → true`的原因是
    - ".*" = ".."所以可以是"ab"
