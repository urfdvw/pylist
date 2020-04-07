# [192. Wildcard Matching](https://www.lintcode.com/problem/wildcard-matching/description)

Implement wildcard pattern matching with support for '?' and '*'.

- '?' Matches any single character.
- '*' Matches any sequence of characters (including the empty sequence).
The matching should cover the entire input string (not partial).

Example 1
```
Input:
"aa"
"a"
Output: false
```
Example 2
```
Input:
"aa"
"aa"
Output: true
```
Example 3
```
Input:
"aaa"
"aa"
Output: false
```
Example 4
```
Input:
"aa"
"*"
Output: true
Explanation: '*' can replace any string
```
Example 5
```
Input:
"aa"
"a*"
Output: true
```
Example 6
```
Input:
"ab"
"?*"
Output: true
Explanation: '?' -> 'a' '*' -> 'b'
```
Example 7
```
Input:
"aab"
"c*a*b"
Output: false
```
Notice
```
1<=|s|, |p| <= 1000
It is guaranteed that 𝑠 only contains lowercase Latin letters and p contains lowercase Latin letters , ? and *
```

# Solution
```python
from functools import lru_cache
class Solution:
    """
    @param s: A string 
    @param p: A string includes "?" and "*"
    @return: is Match?
    """
    def isMatch(self, s, p):
        return self.dp(s, p)
        
    @lru_cache(None)
    def dp(self, s, p):
        if p == '*':
            return True
            
        if s == p:
            return True
            # s == p == "" is here
        
        if len(p) == 0: 
            return False
            # len(s) must not be 0
            
        if p[0] == '*': 
            # this if is necessary, because s='' won't start the for loop,
                # but we still need recursion because p might not end yet
            if len(s) == 0:
                return self.dp(s, p[1:])
                
            for i in range(len(s)):
                if self.dp(s[i:], p[1:]):
                    return True
            return False
            # The only way s = "" and the ans is true is going to be here
        
        if len(s) == 0:
            return False
            
        if s[0] == p[0] or p[0] == '?':
            return self.dp(s[1:], p[1:])
            
        if s[0] != p[0]:
            return False
            
        return False
```
test case
s: "" p:"***"
# care
都写注释了

这个题，条件的前后顺序非常重要。