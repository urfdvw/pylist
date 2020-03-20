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
  - `s[i:j:k]`
- 改
  - `s[i] = x`
  - `s[i:j] = t`
  - `s[i,j,k]  = t`

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
  - `a | b`
  - `a & b`
  - `a - b`
  - `a ^ b`

Data management
- 增
  - `a.add(x)`
- 删
  - `a.remove(x)`
  - `a.discard(x)`
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
  - `d.pop(key)`
  - `d.popitem()`
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
  - `q.remove(x)`
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
  - `q.rotate(n=1)`
  - `q.reverse()`

## heapq
```python
from heapq import heappush, heappop
h = []
heappush(h, 1)
print(heappop())
```

# 常用技巧
用for-else代替flag的使用
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

# 注意事项
- `//` do floor operation to get the int number
  - ```
    >>> 11 // 4
    2
    >>> -11 // 4
    -3
    ```
