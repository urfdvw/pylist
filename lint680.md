# [680. Split String](https://www.lintcode.com/problem/split-string/description)

Give a string, you can choose to split the string after one character or two adjacent characters, and make the string to be composed of only one character or two characters. Output all possible results.

Example1
```
Input: "123"
Output: [["1","2","3"],["12","3"],["1","23"]]
```
Example2
```
Input: "12345"
Output: [["1","23","45"],["12","3","45"],["12","34","5"],["1","2","3","45"],["1","2","34","5"],["1","23","4","5"],["12","3","4","5"],["1","2","3","4","5"]]
```

# DC solution
```python
class Solution:
    """
    @param: : a string to be split
    @return: all possible split string array
    """

    def splitString(self, s):
        return self.dc(s)
        
    def dc(self, s):
        if len(s) == 0:
            return [[]]
        if len(s) == 1:
            return [[s]]
        if len(s) == 2:
            return [[s], [s[0], s[1]]]
        
        ans1 = self.dc(s[1:])
        ans2 = self.dc(s[2:])
        ans = [[s[:1]] + a for a in ans1] + [[s[:2]] + a for a in ans2]
        return ans
```

# Traverse solution
```python
class Solution:
    """
    @param: : a string to be split
    @return: all possible split string array
    """

    def splitString(self, s):
        ans = []
        cur = [] # current
        self.traverse(s, cur, ans)
        return ans
        
    def traverse(self, s, cur, ans):
        if len(s) == 0:
            ans.append(cur[:])
            
        for i in [1, 2]:
            # last i should be len(s)
            if i <= len(s):
                cur.append(s[:i])
                self.traverse(s[i:], cur, ans)
                cur.pop()
        return 
```