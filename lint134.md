# [134. LRU Cache](https://www.lintcode.com/problem/lru-cache/description)

Design and implement a data structure for Least Recently Used (LRU) cache. It should support the following operations: get and set.

- get(key) Get the value (will always be positive) of the key if the key exists in the cache, otherwise return -1.
- set(key, value) Set or insert the value if the key is not already present. When the cache reached its capacity, it should invalidate the least recently used item before inserting a new item.

Finally, you need to return the data from each get.

Example 1:
```
Input:
LRUCache(2)
set(2, 1)
set(1, 1)
get(2)
set(4, 1)
get(1)
get(2)
Output: [1,-1,1]
Explanation：
cache cap is 2，set(2,1)，set(1, 1)，get(2) and return 1，set(4,1) and delete (1,1)，because （1,1）is the least use，get(1) and return -1，get(2) and return 1.
```
Example 2:
```
Input：
LRUCache(1)
set(2, 1)
get(2)
set(3, 2)
get(2)
get(3)
Output：[1,-1,2]
Explanation：
cache cap is 1，set(2,1)，get(2) and return 1，set(3,2) and delete (2,1)，get(2) and return -1，get(3) and return 2.
```
# Solution
```python
class node:
    def __init__(self, key=None, val=None):
        self.key = key
        self.val = val
        self.next = None
        
class LRUCache:
    """
    @param: capacity: An integer
    """
    def __init__(self, capacity):
        self.cap = capacity
        self.previous_node = {}
        self.dummy = node()
        self.end = self.dummy
    
    def list_append(self, new_node):
        # make connection to its previous
        self.previous_node[new_node.key] = self.end
        # make connection to its next
        self.end.next = new_node
        # move the list end
        self.end = new_node
        # make a marker at the tail so that it is an end
        self.end.next = None
    
    def list_pop(self, old_node):
        # if not a node
        if old_node is None:
            return
        # make connection from left to right
        self.previous_node[old_node.key].next = old_node.next
        # make connection from right to left
        if old_node.next is not None:
            self.previous_node[old_node.next.key] = self.previous_node[old_node.key]
        else: # if old node is tail
            self.end = self.previous_node[old_node.key]
        # remove old_node's key from dict()
        del self.previous_node[old_node.key]
        return old_node
        
    def list_kick(self, key):
        # find the node
        the_node = self.previous_node[key].next
        # if it is tail then no need to kick
        if the_node.next is None:
            return
        # pop the_node and append it to right
        self.list_append(self.list_pop(the_node))
        

    """
    @param: key: An integer
    @return: An integer
    """
    def get(self, key):
        # if key not in catch
        if key not in self.previous_node:
            return -1
        # move the related node to the end
        self.list_kick(key)
        # the value of tail should be the answer
        return self.end.val
        

    """
    @param: key: An integer
    @param: value: An integer
    @return: nothing
    """
    def set(self, key, value):
        # if an exsited key
        if key in self.previous_node:
            # move to tail
            self.list_kick(key)
            # set the value again
            self.end.val = value
            return
        # if a new key
        # create a new node
        new_node = node(key, value)
        # append it to tail
        self.list_append(new_node)
        # if over sized
        if len(self.previous_node) > self.cap:
            # pop the first on after dummy
            self.list_pop(self.dummy.next)
        return
```

# Care
- linked list 的构成方法：
    - 单向linked list，只有next， 没有前向指针
    - 必要成员
        - key
        - next
    - end是一个node，有数值， 没有next
    - head是一个dummy node，没有数值，有next
    - previous_node是一个dict，key是当前node的key，value是之前的弄得。它充当两个角色
        - 充当前向指针。
        - 因为有dummy，所以所有有值的node都有previous_node。所以可以充当所有node的随机存取指针
- popleft和kick有重复代码，所以写一个任意位置的pop可以简化kick
- pop本来没必要返回任何值的。但是出于习惯，为了写下`self.list_append(self.list_pop(the_node))`，直接把输入值返回。
