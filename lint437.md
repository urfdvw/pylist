# [437. Copy Books](https://www.lintcode.com/problem/copy-books/description)

Given n books and the i-th book has pages[i] pages. There are k persons to copy these books.

These books list in a row and each person can claim a ***continous*** range of books. For example, one copier can copy the books from i-th to j-th continously, but he can not copy the 1st book, 2nd book and 4th book (without 3rd book).

They start copying books at the same time and they all cost 1 minute to copy 1 page of a book. What's the best strategy to assign books so that the slowest copier can finish at earliest time?

Return the shortest time that the slowest copier spends.

Example 1:
```
Input: pages = [3, 2, 4], k = 2
Output: 5
Explanation: 
    First person spends 5 minutes to copy book 1 and book 2.
    Second person spends 4 minutes to copy book 3.
```
Example 2:
```
Input: pages = [3, 2, 4], k = 3
Output: 4
Explanation: Each person copies one of the books.
```
Challenge
```
O(nk) time
```
## Solution:
```python
class Solution:
    def copyBooks(self, pages, k):
        """
        in: pages: int list: list of numbers of pages 
        in: k: int: number of workers
        out: l: int: shortest time that the slowest copier spends. (total time)
        """
        # corner cases
        if not pages:
            # if empty set, S***, why there is empty set?
            return 0
        if k >= len(pages):
            # if the size of the array is smaller than the number of workers
            return max(pages)
        
        # condition: 
        ## shortest time, that means con(up) should be true
        ## big $l$ means smaller $k$, NoOfWorkerNeeded(pages,up) should be small
        ## "There are k persons" can be seen as "There are at most k persons"
        def con(l): return self.NoOfWorkerNeeded(pages,l) <= k

        # binary search for the smallest l given a desired k
        ## largest possible l is when 1 guy copys all the books
        up = sum(pages)
        ## smallest possible l is when each book has a worker
        low = max(pages)
        # bisection loop
        while(low + 1 < up):
            mid = int((up - low)/2) + low
            if con(mid):
                up = mid
            else:
                low = mid
        # return the shortest time
        return up

    def NoOfWorkerNeeded(self, pages,l):    
        """
        in: pages: int list: same as pages discribed
        in: l: int: total time
        out: k: int: minimum number of workers needed
        """
        accu = 0  # workload accumulater per person
        k = 1  # worker number accumulater
        # k start from one because we need a current worker
        for a in pages:
            if accu + a > l:
                # if one more book is to much for the current worker
                k += 1  # get another worker
                accu = a  # and this book belong to the new worker
            else:
                # if still holdable
                accu += a  # this book belong to the current worker
        return k    
```

special care
- "time that the slowest copier spends" basically means "total time"
- "k persons" means "at most k persons"
- always remember to deal with corner case, ask boss for corner case existence.
- define a abstract function, comment the usage of the function. Then work on the bisection main program. Then try to implement the abstract function.
- take special care on the direction of condition
    - ">=" or "<=", or others
    - con(up) == true or con(low) == true
        - this can be inferred from the question such as "return the largest ...", largest means con(low) == true

---

## Archived solution

```python
class Solution:
    def copyBooks(self, pages, k):
        """
        find the smallest l gives the desired k
        note: smaller l gives larger k
        
        in: pages: int list: list of numbers of pages 
        in: k: int: number of workers
        out: l: int: shortest time that the slowest copier spends. (total time)
        """

        def NoOfWorkerNeeded(pages,l):    
            """
            in: pages: int list: same as pages discribed
            in: l: int: total time
            out: k: int: minimum number of workers needed
            """
            accu = 0  # workload accumulater per person
            k = 1  # worker number accumulater
            # k start from one because we need a current worker
            for a in pages:
                if accu + a > l:
                    # if one more book is to much for the current worker
                    k += 1  # get another worker
                    accu = a  # and this book belong to the new worker
                else:
                    # if still holdable
                    accu += a  # this book belong to the current worker
            return k    

        # corner cases
        if not pages:
            # if empty set, S***, why there is empty set?
            return 0
        if k >= len(pages):
            # if the size of the array is smaller than the number of workers
            return max(pages)

        # binary search for the smallest l given a desired k
        ## largest possible l is when 1 guy copys all the books
        up = sum(pages)
        ## smallest possible l is when each book has a worker
        low = max(pages)
        # search
        while low + 1 < up:
            mid = int((up - low)/2) + low
            k_ = NoOfWorkerNeeded(pages,mid)
            if  k_ > k:
                # which means mid is too small
                low = mid
            if k_ == k:
                # as we want the smallest l
                # mid might be smaller
                up = mid
            if k_ < k:
                # which means mid is too large
                up = mid
        # check wether up or low
        ## because we want the smallest l, check the small one
        if NoOfWorkerNeeded(pages, low) == k:
            return low
        else:
            return up
```
question
- 先判断up和先判断low好像都能通过，不知为何。