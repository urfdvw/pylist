# [146. LRU Cache](https://leetcode.com/problems/lru-cache/)

Design and implement a data structure for Least Recently Used (LRU) cache. It should support the following operations: get and put.

get(key) - Get the value (will always be positive) of the key if the key exists in the cache, otherwise return -1.
put(key, value) - Set or insert the value if the key is not already present. When the cache reached its capacity, it should invalidate the least recently used item before inserting a new item.

The cache is initialized with a positive capacity.

Follow up:

    Could you do both operations in O(1) time complexity?

Example:

    LRUCache cache = new LRUCache( 2 /* capacity */ );

    cache.put(1, 1);
    cache.put(2, 2);
    cache.get(1);       // returns 1
    cache.put(3, 3);    // evicts key 2
    cache.get(2);       // returns -1 (not found)
    cache.put(4, 4);    // evicts key 1
    cache.get(1);       // returns -1 (not found)
    cache.get(3);       // returns 3
    cache.get(4);       // returns 4

# Solution
```python
class Node:
    
    def __init__(self, key, val):
        self.key = key
        self.val = val
        self.next = None

class LRUCache:

    def __init__(self, capacity: int):
        self.N = capacity
        self.len = 0
        # head: old node, end: new node
        self.head = Node(None, None)
        self.end = self.head
        # key: key of a Node; Val: previous Node
        self.previous = dict() 
        
    def list_pop(self, key):
        val = self.previous[key].next.val
        previous_node = self.previous[key]
        next_node = previous_node.next.next # Maybe None
        # del key in dict
        del self.previous[key]
        # link from previous to next
        previous_node.next = next_node
        # link from next to previous, if next exist
        if next_node is not None: # if poped self.end
            self.previous[next_node.key] = previous_node
        else:
            self.end = previous_node
        self.len -= 1
        return val
        
    def list_append(self, key, val):
        self.end.next = Node(key, val)
        self.previous[key] = self.end
        self.end = self.end.next
        self.len += 1
        
    def get(self, key: int) -> int:
        # assert key in queue
        if key not in self.previous:
            return -1
        # pop the node
        val = self.list_pop(key)
        self.list_append(key, val)        
        return val

    def put(self, key: int, val: int) -> None:
        # if key in queue, pop then append updated node
        if key in self.previous:
            self.list_pop(key)
        self.list_append(key, val)
        # overflow control
        if self.len > self.N:
            self.list_pop(self.head.next.key)
            
# Your LRUCache object will be instantiated and called as such:
# obj = LRUCache(capacity)
# param_1 = obj.get(key)
# obj.put(key,value)
```

# Care
- 一定切记，定义新的数据格式的时候，要么新定义一个class，要么写好接口再用，否则很容易糊粥。
- 又有一个拼写错误