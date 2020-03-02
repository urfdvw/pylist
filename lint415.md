# [415. Valid Palindrome](https://www.lintcode.com/problem/valid-palindrome/description)
Given a string, determine if it is a palindrome, considering only alphanumeric characters and ignoring cases.

Have you consider that the string might be empty? This is a good question to ask during an interview.

For the purpose of this problem, we define empty string as valid palindrome.

Example 1:
```
Input: "A man, a plan, a canal: Panama"
Output: true
Explanation: "amanaplanacanalpanama"
```
Example 2:
```
Input: "race a car"
Output: false
Explanation: "raceacar"
```
Challenge
```
O(n) time without extra memory.
```

# thinking
- corner case are defined by whether the algorithm can be started, we need two pointers, so the string must be longer than 2
- there are two ways to move the pointers
    - if not letter
    - if letter are same
- return False if different found, else True
- loop when `up > low`

# Solution
```python
class Solution:
    """
    @param s: A string
    @return: Whether the string is a valid palindrome
    """
    def isPalindrome(self, s):
        # corner case
        if len(s) <= 1:
            return True
        # init 2 pointers
        low = 0
        up = len(s) - 1
        # while not meet
        while up > low:
            # case 1 low is not letter
            if not (s[low].isalpha() or s[low].isdigit()):
                low += 1
                continue
            
            # case 2 up is not letter
            if not (s[up].isalpha() or s[up].isdigit()):
                up -= 1
                continue
            
            # case 3 same letter
            if s[up].lower() == s[low].lower():
                up -= 1
                low += 1
            else: # if difference found
                return False
        # return true if no difference found
        return True
```

# special care
- 由于没挪动一次指针，都需要判断一次while的条件，所以每挪动一步指针都continue一下
- 相同字母情况同时挪动两个指针，可能会重叠退出，也可能会交错退出，但都是完整走完了全部字符串。
    - 因为每次不确定是挪动几个指针，所以不方便用相邻退出。