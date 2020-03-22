# [209. First Unique Character in a String](https://www.lintcode.com/problem/first-unique-character-in-a-string/description)

Find the first unique character in a given string. You can assume that there is at least one unique character in the string.

Example
```
Example 1:
	Input: "abaccdeff"
	Output:  'b'
	
	Explanation:
	There is only one 'b' and it is the first one.


Example 2:
	Input: "aabccd"
	Output:  'b'
	
	Explanation:
	'b' is the first one.
```
# Solution
```python
class Solution:
    """
    @param str: str: the given string
    @return: char: the first unique character in a given string
    """
    def firstUniqChar(self, str):
        # the alphabet as a string
        alphabet = 'abcdefghijklmnopqrstuvwxyz'
        # map letters to numbers 0~25
        l2d = dict()
        for i in range(26):
            l2d[alphabet[i]] = i
        # record the positin of occurence of letters in str
        positions = [[] for i in range(26)]
        for i, char in enumerate(str):
            positions[l2d[char]].append(i)
        # find the letters with only 1 occurence
        letter_once = [[p[0], alphabet[i]] for i, p in enumerate(positions) if len(p) == 1]
        # find the letter with the min position
        ans = min(letter_once)
        return ans[1]
```
# care
- 可以用list的时候就不用dict。因为list的功能更多。比如这里的min