# [200. Longest Palindromic Substring](https://www.lintcode.com/problem/longest-palindromic-substring/description)

Given a string S, find the longest palindromic substring in S. You may assume that the maximum length of S is 1000, and there exists one unique longest palindromic substring.

Example 1:
```
Input:"abcdzdcab"
Output:"cdzdc"
```
Example 2:
```
Input:"aba"
Output:"aba"
```

# Solution
```python
class Solution:
    """
    @param s: input string
    @return: the longest palindromic substring
    """
    def longestPalindrome(self, s):
        if len(s) <= 1:
            return s
            
        start_odd, end_odd, len_odd = self.check(s, 0)
        start_even, end_even, len_even = self.check(s, 1)
        print(start_even, end_even, len_even, start_odd, end_odd, len_odd)
        
        len_out = max([len_odd, len_even])
        if len_out == len_odd:
            return s[start_odd: end_odd + 1]
            
        if len_out == len_even:
            return s[start_even: end_even + 1]
        
    def check(self, s, offset):
        longest_len = -1
        longest_start = None
        longest_end = None
        
        for center in range(len(s) - offset):
            wing = 0
            while True:
                # calculate range and length
                start = center - wing
                end = center + offset + wing
                length = end - start + 1
                # if not equal end Palindrome
                if s[start] != s[end]:
                    break
                # if still Palindrome
                ## record range and length
                if length > longest_len:
                    longest_len = length
                    longest_start = start
                    longest_end = end
                ## extend
                if self.in_boundary(s, start - 1) and self.in_boundary(s, end + 1):
                    wing += 1
                else:
                    break
        return longest_start, longest_end, longest_len
        
    def in_boundary(self, s, i):
        return i >= 0 and i < len(s)
```

# Special Care
- 这题的很多地方是TAMA瞎试出来的，非常不优雅。
- even和odd合成一个函数其实非常费劲。
