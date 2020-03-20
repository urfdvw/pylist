# [13. Implement strStr()](https://www.lintcode.com/problem/implement-strstr/description)

For a given source string and a target string, you should output the first index(from 0) of target string in source string.

If target does not exist in source, just return -1.

Example 1:
```
Input: source = "source" ，target = "target"
Output: -1	
Explanation: If the source does not contain the target content, return - 1.
```
Example 2:
```
Input:source = "abcdabcdefg" ，target = "bcd"
Output: 1	
Explanation: If the source contains the target content, return the location where the target first appeared in the source.
```
# Solution
```python
class Solution:
    """
    @param source: 
    @param target: 
    @return: return the index
    """
    def strStr(self, source, target):
        # corner cases
        if target == '':
            return 0
            
        # loop of start position
        for i in range(len(source) - len(target) + 1):
            for j in range(len(target)):
                if source[i+j] != target[j]:
                    break
            else: # if no difference found
                return i
                
        # if failed to return at any starting position
        return -1
```

# questions to ask
- Q: What shoul I return if target is ""
    - A: 0
# special care
- use special case to se range:
    - if len(s) and len(t) are the same, it should run and only run once.