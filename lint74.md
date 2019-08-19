# [74. First Bad Version](https://www.lintcode.com/problem/first-bad-version/description)
The code base version is an integer start from 1 to n. One day, someone committed a bad version in the code case, so it caused this version and the following versions are all failed in the unit tests. Find the first bad version.

You can call isBadVersion to help you determine which version is the first bad one. The details interface can be found in the code's annotation part.

Example
```
Given n = 5:

    isBadVersion(3) -> false
    isBadVersion(5) -> true
    isBadVersion(4) -> true

Here we are 100% sure that the 4th version is the first bad version.
```

Challenge
```
You should call isBadVersion as few as possible.
```

## Solution
```python
#class SVNRepo:
#    @classmethod
#    def isBadVersion(cls, id)
#        # Run unit tests to check whether verison `id` is a bad version
#        # return true if unit tests passed else false.
# You can use SVNRepo.isBadVersion(10) to check whether version 10 is a 
# bad version.
class Solution:
    """
    @param n: An integer
    @return: An integer which is the first bad version.
    """
    def findFirstBadVersion(self, n):
        # check out questions:
        ## is n>1 always true? Yes!
        ## is there always a bad version? Yes!
        ## is there always a good version? No!
        
        # corner cases
        ## no corner case for special "n"
        ## if no good versions
        if SVNRepo.isBadVersion(1):
            return 1
        
        # init boundaries
        up = n # bad end
        low = 1 # good end
        while low + 1 < up:
            # while up and low are not next to each other
            mid = int(low + (up - low)/2)
            if SVNRepo.isBadVersion(mid):
                # keep bad end bad
                up = mid
            else:
                low = mid
                
        # check wether up or low
        ## must be up, the first one exceed boundary
        return up
    
        # if not found
        ## if bad version exists, no not found case
```
special care
- let's call 'good' and 'bad' properties
- corner cases are uniform properties: all good or all bad
- because there are only 2 properties, only 2 cases of comparison, keep the properties of *up* and *low*, instead of ">, <, =="
- return does not need check, use the property 

[Binary search notes](readme.md#Binary-search)