# Python 库函数背诵树

## Sequence (list, tuple)
Data management: non-slicing style
- 增
  - `s.append(x)`
  - `s.extend(t)` or `s += t`
  - `s.insert(i, x)`
- 删
  - `s.pop([i])`
  - `s.remove(x)`
  - `s.clear()`
- 查
  - summary
    - `len(s)`
    - `max(s)`
    - `min(s)`
  - existence
    - `x in s`
  - edit find
    - `s.index(x[, i[, j]])`
    - `s.count(x)`
- 改
  - `s.reverse()`

Data management: slicing Style
- 增
  - `s[i:i] = t`
    - append: `s[len(s):len(s)] = [x]`
    - extend: `s[len(s):len(s)] = t`
    - insert: `s[i:i] = [x]`
- 删
  - `del s[i]`
  - `del s[i:j]`
  - `del s[i:j:k]` 
- 查
  - `s[i]`
  - `s[i:j]` 
  - `s[i:j:k]` 越界自动停止
- 改
  - `s[i] = x`
  - `s[i:j] = t` 大小不需要一致
  - `s[i,j,k]  = t` 大小必须一致

数学运算
- 加减乘除
  - `a + b`
  - *shalow copy is not very often used*

## Set
数学运算
- 比较
  - `a.isdisjoint(b)`
  - `a <= b`
  - `a < b`
  - `a >= b`
- 加减乘除
  - `a | b` or
  - `a & b` and
  - `a - b` difference
  - `a ^ b` symetric difference

Data management
- 增
  - `a.add(x)`
- 删
  - `a.remove(x)` will raise error
  - `a.discard(x)` will not raise error if key not exist
  - `a.pop()`
  - `a.clear()`
- 查
  - summary
    - `len(a)`
    - `max(a)`
    - `min(a)`
  - existence
    - `x in a`
- 改
  - `a |= b`
  - `a &= b`
  - `a -= b`
  - `a ^= b`

## Dict

Data management
- 增
  - `d[key] = value`
- 删
  - `del d[key]`
  - `d.pop(key)` return value
  - `d.popitem()` for distruction
  - `a.clear()`
- 查
  - iteration
    - `d.items()`
    - `d.keys()`
    - `d.values()`
    - `iter(d)` or `iter(d.keys())`
  - summary
    - `len(d)`
    - `max(d)` max key
    - `min(d)` min key
  - existence
    - `key in d`
- 改
  - `d[key] = value`
  - `d1.update(d2)`
  - `reversed(d)` 等同于 `reversed(d.keys())`

关于方向
- 3.7 和之后，dict 的 iterator 将会按照加入的顺序
  - 新加入才算
  - 修改不算
  - 删除后再加入算新加入

- 3.8 和之后，dict 可以 reverse
- `set()`没有方向

Operations with defaults
- `d.get(key[, default])`
- `d.setdefault(key[, default])`
  - `d.setdefault(key, []).append(item)`
  - 然而不能 ~~`d.setdefault(key, 0).add(1)`~~，因为`add`不是inplace
- `pop(key[, default])`

## deque
```python
from collections import deque
```

- 增
  - `q.append(x)`
  - `q.extend(t)`
  - `q.appendleft(x)`
  - `q.extendleft(t)`
  - `q.insert(i, x)`
- 删
  - `q.pop()`
  - `q.popleft()`
  - `q.remove(x)` O(n) time complexity
- 查
  - `q[i]`
    `q[0]` and `q[-1]` peek
  - edit find
    - `q.count(x)`
    - `q.index(x[, start[, stop]])`
  - summary
    - `len(q)`
    - `max(q)`
    - `min(q)`
    - `q.maxlen` not a function
  - existence
    - `x in q`
- 改
  - `q.rotate(n=1)` O(n) time complexity
  - `q.reverse()`

## heapq
```python
from heapq import heapify, heappush, heappop
h = ***
heapify(h)
heappush(h, x)
x = heappop(h)
print(h[0]) # peek
```
max heap 的 负号位置
```python
h = [-x for x in array]
heapify(h)
heappush(h, -x)
x = -heappop(h)
print(-h[0]) # peek
```

# 常用技巧
## 用for-else代替flag的使用
```python
for item in container:
    if search_something(item):
        # Found it!
        process(item)
        break
else:
    # Didn't find anything..
    not_found_in_container()
```
## Lambda function
```python
fun1 = lambda x: -x * 10
print(fun1(1))
```
```
-10
```
same as 
```python
def fun2(x): return -x * 10
print(fun2(1))
```
```
-10
```
in sorting
```python
a = [1, 4, -1, -3]
print(sorted(a))
print(sorted(a, key=fun1))
print(a)
print(a.sort(key=fun2))
print(a)
```
```
[-3, -1, 1, 4]
[4, 1, -1, -3]
[1, 4, -1, -3]
None
[4, 1, -1, -3]
```
`a.sort()` won't return anything
```python
ab = {'a':1, 'b':2, 'c': 4, 'd':3}
data = 'babdc'
data.sort()
```
```
      1 ab = {'a':1, 'b':2, 'c': 4, 'd':3}
      2 data = 'babdc'
----> 3 data.sort()

AttributeError: 'str' object has no attribute 'sort'
```
```python
print(sorted(data))
print(sorted(data, key=lambda x: ab[x]))
```
```
['a', 'b', 'b', 'c', 'd']
['a', 'b', 'b', 'd', 'c']
```
# Sort table
List 是可以按元素直接比较的，左边的权重高。
所以List of List 是可以直接sort的。
也可以取最值。
也可以heap。

[详情](sort_table.ipynb)

Example
- [209. First Unique Character in a String](lint209.md)
- [612. K Closest Points](lint612.md)

# key in heap
`heappush()` and `heappop` does not have `key` attr. Need to define a `__lt__()` function for the same propose

```python
from heapq import heappush, heappop
# self defined value
ab = {'a':1, 'b':2, 'c': 4, 'd':3}
# data
data = 'babdc'
# char class to define the comparison function
class char:
    def __init__(self, val):
        self.val = val
    def __lt__(self, other):
        if ab[self.val] < ab[other.val]:
            return True
        else:
            return False
# heap sort
h = []
for c in data:
    heappush(h, char(c))
ans = []
while h:
    ans.append(heappop(h).val)
print(ans)
```
```
['a', 'b', 'b', 'd', 'c']
```

# Zip
zip 的操作是把同index放在一个tuple里，所以和转置息息相关。
注意zip的输出不是list，而是一个zip，可用作iter

使用zip函数转置list of tuples
```python
# Python3 code to demonstrate  
# Unzip a list of tuples 
# using zip() and * operator 
  
# initializing list of tuples 
test_list = [('Akshat', 1), ('Bro', 2), ('is', 3), ('Placed', 4)] 
  
# Printing original list 
print ("Original list is : " + str(test_list)) 
  
# using zip() and * operator to 
# perform Unzipping 
res = list(zip(*test_list)) 
      
# Printing modified list  
print ("Modified list is : " + str(res)) 
```
```
Original list is : [('Akshat', 1), ('Bro', 2), ('is', 3), ('Placed', 4)]
Modified list is : [('Akshat', 'Bro', 'is', 'Placed'), (1, 2, 3, 4)]
```


# 注意事项
- `//` do floor operation to get the int number
  - ```
    >>> 11 // 4
    2
    >>> -11 // 4
    -3
    ```
