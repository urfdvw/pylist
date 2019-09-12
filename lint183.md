# [183. Wood Cut](https://www.lintcode.com/problem/wood-cut/description)
Given n pieces of wood with length L[i] (integer array). Cut them into small pieces to guarantee you could have ***equal or more than k*** pieces with the same length. What is the longest length you can get from the n pieces of wood? Given L & k, return the ***maximum*** length of the small pieces.

You couldn't cut wood into float length. If you couldn't get >= k pieces, return 0.

Example 1:
```
Input:
L = [232, 124, 456]
k = 7
Output: 114
Explanation: We can cut it into 7 pieces if any piece is 114cm long, however we can't cut it into 7 pieces if any piece is 115cm long.
```

Example 2:
```
Input:
L = [1, 2, 3]
k = 7
Output: 0
Explanation: It is obvious we can't make it.
```

Challenge
```
O(n log Len), where Len is the longest length of the wood.
```

## Solution
```python
class Solution:
    def woodCut(self, L, k):
        """ backward problem
        in
            L: list of int: wood length list
            k: int: desire number of pieces
        out
            u: int: Length of the small pieces
        """ 

        # corner cases
        ## couldn't get >= k pieces
        if sum(L) < k:
            return 0

        # condition, con(low) should be true
        ## equal or more than k pieces
        def con(u): return self.n_of_pieces_given_length(L, u) >= k
        
        # init up and low
        up = max(L)  # largest possible u, when only 1 piece is cut
        low = 1  # smallest possible u, when smesh everything to pieces
        # bicestion loop
        while low + 1 < up:
            mid = int((up - low)/2 + low)
            if con(mid):
                low = mid
            else:
                up = mid
        
        # return the lagest u that satisfied the condition
        return low
        
    def n_of_pieces_given_length(self, L, u):
        """ foward problem 
        try to cut woods according to given length $u$
        and see how many pieces $k$ we can get
        
        in
            L: list of int: wood length list
            u: int: required piece length
        out
            k: int: total number of pieces
        """
        
        N = [int(l/u) for l in L]
        return sum(N)
```
questions to ask:
- what is the lowest possible u? 1!

special care:
- for better read flow, define the help function as another class method.
- it is worthy to spend more time on the corner cases and also up and low bounds.

---

## Archived solution

```python
class Solution:
    def woodCut(self, L, k):
        """ backward problem
        in
            L: list of int: wood length list
            k: int: desire number of pieces
        out
            u: int: Length of the small pieces
        """ 

        # corner cases
        ## couldn't get >= k pieces
        if sum(L) < k:
            return 0

        # bisection
        ## find the largest $u$ possible that gives $k$
        ## the larger u is, the smaller k is
        up = max(L)  # largest possible u
        low = 1  # smallest possible u
        while(low + 1 < up):
            mid = int((up - low)/2 + low)
            n = self.n_of_pieces_given_length(L, mid)
            if n > k:
                # n is too big => mid is too small => mid should be larger
                low = mid
            if n == k:
                # largest u is desired, mid might be larger
                low = mid
            if n < k:
                # n is too small => mid is too big => mid should be smaller
                up = mid

        # decide up or low
        ## as we want largest u, check up first
        if self.n_of_pieces_given_length(L, up) == k:
            return up
        else:
            return low
        
    def n_of_pieces_given_length(self, L, u):
        """ foward problem 
        try to cut woods according to given length $u$
        and see how many pieces $k$ we can get
        
        in
            L: list of int: wood length list
            u: int: required piece length
        out
            k: int: total number of pieces
        """
        
        N = [int(l/u) for l in L]
        return sum(N)   
```