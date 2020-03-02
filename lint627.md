# [627. Longest Palindrome](https://www.lintcode.com/problem/longest-palindrome/description)

Given a string which consists of lowercase or uppercase letters, find the length of the longest palindromes that can be built with those letters.

This is case sensitive, for example "Aa" is not considered a palindrome here.

Assume the length of given string will not exceed 100000.

Example

```
Input : s = "abccccdd"
Output : 7
Explanation :
One longest palindrome that can be built is "dccaccd", whose length is `7`.
```

# Solution

```python
class Solution:
    """
    @param s: a string which consists of lowercase or uppercase letters
    @return: the length of the longest palindromes that can be built
    """
    def longestPalindrome(self, s):
        # counte occurance of letters
        letter_count = dict() # a counter
        for l in s:
            letter_count.setdefault(l, 0)
            letter_count[l] += 1
        
        # see if there is any odd countings
        for n in letter_count.values():
            if n // 2 * 2 != n: # if n odd
                has_odd = True
                break
        else:
            has_odd = False
        
        # counting
        if has_odd:
            length = 0 # length of the longest palindromes init
            for n in letter_count.values():
                length += n // 2 * 2
            return length + 1
        else: # if no odd countings, just return the sum
            return sum(list(letter_count.values()))
```

# Special Care
- `setdefault(l, 0).add()` will return the answer instead of inplace operation.
- `setdefault(l, 0) += 1` will raise an error
- `letter_count.values()` returns an iterator
- `//` do floor operation to get the int number
  - ```
    >>> 11 // 4
    2
    >>> -11 // 4
    -3
    ```