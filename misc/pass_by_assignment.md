# What is pass by assignment
Python的函数传递方式叫做 Pass by assignment.
为了解释清楚这件事，我们需要先搞清其他几件事1， Python变量的存储形式
至少有三部分
- 值
- 地址， 同一个地址就是同一个变量 is
- 名字

```python
a = 1
```


```python
# value
a
```




    1




```python
# address
id(a)
```




    140232989897472




```python
# a is the name
```
2，Python 中 `=` 的意思是
- 给等号右边的部分起一个名称
- 叫左边这个名字

```python
# give the variable at id(a) a new name called b
# one variable, two name
b = a
id(b)
```




    140232989897472


*，那`a = 1` 发生了什么
- 常量也是有地址的，因为是一个对象
    - 但是如果不命名就释放了

```python
# https://stackoverflow.com/a/15012814/7037749
from _ctypes import PyObj_FromPtr as di
from time import sleep
import sys

wild_id = id(12736)
print(wild_id)
print(di(wild_id))
```

    140232939653648
    12736



```python
# print(di(wild_id)) # the content changed, thanks to garbage collector
```


```python
id(1) # id of small ints are fixed
```




    140232989897472




```python
a = 1
id(a)
```




    140232989897472




```python
a is 1
```




    True



3, 如果一个变量有多个名字，那么通过一个名字修改的话，用其他名字访问到的值也应该是改变的
- 但是前提是这个变量是 immutable 的

3.1 如果修改一个 immutable 的变量，其实是
- 计算出新的变量
- 把名字冠给新的变量
- 名字还是原来的名字，变量不再是原来的变量了

3.2 如果修改一个 mutable 的变量
- 如果是 inplace 修改，两个名字就还是对应同一个变量
- 如果涉及到 = 那很可能就变了


```python
a = 1
b = a
print(a, b)
b = b + 1
print(a, b)
```

    1 1
    1 2



```python
a = [3, 5, 2, 1, 4]
b = a
print(a, b)
b = sorted(b)
print(a, b)
```

    [3, 5, 2, 1, 4] [3, 5, 2, 1, 4]
    [3, 5, 2, 1, 4] [1, 2, 3, 4, 5]



```python
a = [3, 5, 2, 1, 4]
b = a
print(a, b)
b.sort()
print(a, b)
```

    [3, 5, 2, 1, 4] [3, 5, 2, 1, 4]
    [1, 2, 3, 4, 5] [1, 2, 3, 4, 5]

3.3 `+=` 是 inplace 吗
- 得看 class 的 __iadd__() 的实现形式，不能一概而论

- 但是根据 python 的官方设定
    - mutable 的 += 是 inplace
    - immutable 的 += 不是

```python
a = [1, 2]
b = a
b += [4, 3]
print(a, b)
```

    [1, 2, 4, 3] [1, 2, 4, 3]



```python
a = (1, 2)
b = a
b += (4, 3)
print(a, b)
```

    (1, 2) (1, 2, 4, 3)

函数的参数传递相当于经历了一次 `=`

```python
def f(x, y):
    x += y
    print('x , y =', x, ',', y)
```


```python
# immutable example
a, b = 1, 2
f(a, b)
print('a , b =', a, ',', b)
```

    x , y = 3 , 2
    a , b = 1 , 2



```python
a, b = 1, 2
x, y = a, b
x += y
print('x , y =', x, ',', y)
print('a , b =', a, ',', b)
```

    x , y = 3 , 2
    a , b = 1 , 2



```python
# mutable example
import numpy as np
a, b = np.array(1), np.array(2)
f(a, b)
print('a , b =', a, ',', b)
```

    x , y = 3 , 2
    a , b = 3 , 2



```python
a, b = np.array(1), np.array(2)
x, y = a, b
x += y
print('x , y =', x, ',', y)
print('a , b =', a, ',', b)
```

    x , y = 3 , 2
    a , b = 3 , 2

同样的事情也发生在 for loop

```python
l = [1, 2, 3]
for item in l:
    item += 1
print(l)
```

    [1, 2, 3]



```python
l = [1, 2, 3]
# for loop
item = l[0] # is a list, immutable
item += 1
item = l[1]
item += 1
item = l[2]
item += 1
# end for loop
print(l)
```

    [1, 2, 3]



```python
l = [[1], [2], [3]]
for item in l:
    item[0] += 1
print(l)
```

    [[2], [3], [4]]



```python
l = [[1], [2], [3]]
# for loop
item = l[0] # is a list, mutable
item[0] += 1
item = l[1]
item[0] += 1
item = l[2]
item[0] += 1
# end for loop
print(l)
```

    [[2], [3], [4]]



```python

```
