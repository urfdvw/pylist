# [844. Backspace String Compare](https://leetcode.com/problems/backspace-string-compare/)

Given two strings S and T, return if they are equal when both are typed into empty text editors. # means a backspace character.

Note that after backspacing an empty text, the text will continue empty.

Example 1:

    Input: S = "ab#c", T = "ad#c"
    Output: true
    Explanation: Both S and T become "ac".
Example 2:

    Input: S = "ab##", T = "c#d#"
    Output: true
    Explanation: Both S and T become "".
Example 3:

    Input: S = "a##c", T = "#a#c"
    Output: true
    Explanation: Both S and T become "c".
Example 4:

    Input: S = "a#c", T = "b"
    Output: false
    Explanation: S becomes "c" while T becomes "b".
Note:

    1 <= S.length <= 200
    1 <= T.length <= 200
    S and T only contain lowercase letters and '#' characters.
Follow up:

    Can you solve it in O(N) time and O(1) space?

# Solution

Simulation Solution

```python
class Solution:
    def backspaceCompare(self, S: str, T: str) -> bool:
        return self.str2list(S) == self.str2list(T)
        
    def str2list(self, stri):
        ans = []
        for c in stri:
            if c == '#':
                if len(ans) > 0:
                    ans.pop()
            else:
                ans.append(c)
        return ans
```

Pointer Solution
```python
class Solution:
    def backspaceCompare(self, S: str, T: str) -> bool:
        i = len(S) - 1
        j = len(T) - 1
        while True:
            i = self.move_cursor(S, i)
            j = self.move_cursor(T, j)
            
            # Stop condition
            if min(i, j) < 0:
                if i < 0  and j < 0:
                    return True
                else:
                    return False
            
            # main logic
            if S[i] == T[j]:
                i -= 1
                j -= 1
                continue
            else: 
                return False
            
            
    def move_cursor(self, S, i):
        """
        move cursor i to the position of next char
        """
        n_sharp = 0
        while i >= 0:
            if S[i] == '#':
                n_sharp += 1
                i -= 1
                continue
            # S[i] != '#' :
            
            if n_sharp > 0:
                i -= 1
                n_sharp -= 1
                continue
            # n_sharp == 0 :
            
            break
        return i
```

# Care
- 这个题有两个思路
    - simulation，模拟按键把字符串生成出来，然后比较
    - pointer，不生成出来，而是挪动指针逐个比较
    - 很明显时间复杂度一样都是O(n)，然而指针更省空间。但是写指针的时候我没写出来。
- 本题目犯的常规错误
    - 引用函数忘了加 `self.`
- 关于指针的教训
    - 不要把两个指针的循环条件同时放入，while循环的条件，否则会非常麻烦。而是要为两个指针单独写while循环
    - while循环的条件要是搞不清楚的话，就直接写`while True:`然后中间break，如果发现条件比较清楚的时候再放回正确的位置，如果不能的话就不改了。
        - 死循环不是一个好的style，实在不行可以换成for一个大数
    - 一个循环只做一件事，这个非常重要。做完就要continue或者break或者return。否则会糊粥。
    - **Style**: 多个if重叠的时候，可以在if之后加入注释，注明如果可以运行到注释这行，需要达到的条件。