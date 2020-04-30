# [678. Valid Parenthesis String](https://leetcode.com/problems/valid-parenthesis-string/)

Given a string containing only three types of characters: '(', ')' and '*', write a function to check whether this string is valid. We define the validity of a string by these rules:

1. Any left parenthesis '(' must have a corresponding right parenthesis ')'.
2. Any right parenthesis ')' must have a corresponding left parenthesis '('.
3. Left parenthesis '(' must go before the corresponding right parenthesis ')'.
4. '*' could be treated as a single right parenthesis ')' or a single left parenthesis '(' or an empty string.
5. An empty string is also valid.

Example 1:

    Input: "()"
    Output: True
Example 2:

    Input: "(*)"
    Output: True
Example 3:

    Input: "(*))"
    Output: True

Note:

    The string size will be in the range [1, 100].
# Solution
```python
from collections import deque
class Solution:
    def checkValidString(self, s: str) -> bool:
        star = deque()
        left = deque()
        for i in range(len(s)):
            if s[i] == '*':
                star.append(i)
                continue
            # s[i] != '*':
            
            if s[i] == '(':
                left.append(i)
                continue
            # s[i] != '('
            
            # s[i] == ')':
            if len(left) > 0:
                left.pop()
                continue
            # left is empty:
            
            if len(star) > 0:
                star.pop()
                continue
            # star is empty:
            
            return False
        
        if len(left) == 0:
            return True
        
        # redundant code for speed
        if len(star) < len(left):
            return False
        
        # (*
        stack = 0
        while len(star) + len(left) > 0:
            if len(star) == 0:
                left.popleft()
                stack += 1
                continue
            if len(left) == 0:
                star.popleft()
                if stack > 0:
                    stack -= 1
                continue
            if left[0] < star[0]:
                left.popleft()
                stack += 1
                continue
            if star[0] < left[0]:
                star.popleft()
                if stack > 0:
                    stack -= 1
                continue
            
        if stack == 0:
            return True
        return False
```