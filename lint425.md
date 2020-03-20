# [425. Letter Combinations of a Phone Number](https://www.lintcode.com/problem/letter-combinations-of-a-phone-number/description)

Given a digit string excluded '0' and '1', return all possible letter combinations that the number could represent.

A mapping of digit to letters (just like on the telephone buttons) is given below.
![T9 keyboard](https://cf.ydcdn.net/latest/images/computer/T9.GIF "T9 keyboard")

Example 1:
```
Input: "23"
Output: ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"]
Explanation: 
'2' could be 'a', 'b' or 'c'
'3' could be 'd', 'e' or 'f'
```
Example 2:
```
Input: "5"
Output: ["j", "k", "l"]
```

# Iteration Solution
```python
class Solution:
    """
    @param digits: A digital string
    @return: all posible letter combinations
    """
    def letterCombinations(self, digits):
        if len(digits) == 0:
            return []
            
        d2l = dict()
        d2l['2'] = ['a', 'b', 'c']
        d2l['3'] = ['d', 'e', 'f']
        d2l['4'] = ['g', 'h', 'i']
        d2l['5'] = ['j', 'k', 'l']
        d2l['6'] = ['m', 'n', 'o']
        d2l['7'] = ['p', 'q', 'r', 's']
        d2l['8'] = ['t', 'u', 'v']
        d2l['9'] = ['w', 'x', 'y', 'z']
        
        ans = ['']
        temp = []
        for d in digits:
            for l in d2l[d]:
                temp += [a + l for a in ans]
            ans = temp
            temp = []
            
        return ans
```