# [49. Group Anagrams](https://leetcode.com/problems/group-anagrams/)

Given an array of strings, group anagrams together.

Example:

    Input: ["eat", "tea", "tan", "ate", "nat", "bat"],
    Output:
    [
    ["ate","eat","tea"],
    ["nat","tan"],
    ["bat"]
    ]
Note:

    All inputs will be in lowercase.
    The order of your output does not matter.

# solution
```python
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        record = dict()
        for s in strs:
            record.setdefault(''.join(sorted(s)), []).append(s)
        ans = [v for v in record.values()]
        return ans
```

# Care
- string sort过之后是list
- list不能作为dict的key