# [228. Middle of Linked List](https://www.lintcode.com/problem/middle-of-linked-list/description)
Find the middle node of a linked list.

Example 1:
```
Input:  1->2->3
Output: 2	
Explanation: return the value of the middle node.
```
Example 2:
```
Input:  1->2
Output: 1	
Explanation: If the length of list is  even return the value of center left one.	
```
Challenge
```
If the linked list is in a data stream, can you find the middle without iterating the linked list again?
```
# Solution
```python
"""
Definition of ListNode
class ListNode(object):
    def __init__(self, val, next=None):
        self.val = val
        self.next = next
"""

class Solution:
    """
    @param head: the head of linked list.
    @return: a middle node of the linked list
    """
    def middleNode(self, head):
        # corner cases
        if head is None: # insane
            return None
        if head.next is None:
            return head
        # init 2 pointers
        slow = head
        fast = head.next
        # move pointers
        odd = True
        while True:
            if fast.next == None:
                return slow
            
            if odd:
                fast = fast.next
                slow = slow.next
            else:
                fast = fast.next
                
            odd = not odd
```
# special care
- 本题的核心在于怎么不错位，预防不错位的方法，就是尽量每次只走一步。
    - 所以不是 ~~快指针走两步，慢指针走一步~~
    - 而是，快指针每次都走一步，慢指针两个循环走一步