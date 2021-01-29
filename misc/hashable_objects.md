# Hashable Objectable
重点：hashable 与否取决于 __hash__() 函数是否被实现，和其他的无关。1， 对于系统自带的数据类型，
immutable 的数据类型都是 hashable 的，反之都不是。
然而这个不是技术原因，而是习惯原因。

```python
hash(int())
```




    0




```python
hash(float())
```




    0




```python
hash(str())
```




    0




```python
hash(bool())
```




    0




```python
hash(tuple())
```




    3527539




```python
hash(list())
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-6-3e2eb619e4e4> in <module>
    ----> 1 hash(list())
    

    TypeError: unhashable type: 'list'



```python
hash(set())
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-7-2699417ebeac> in <module>
    ----> 1 hash(set())
    

    TypeError: unhashable type: 'set'



```python
hash(dict())
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-8-7762fff637c6> in <module>
    ----> 1 hash(dict())
    

    TypeError: unhashable type: 'dict'

2，自定义的 class 的 object 都是 hashable。
默认的 __hash__(self) 的实现是 id(self) // 16

```python
class my_class(object): pass
o = my_class()
print(hash(o))
print(id(o))
print(id(o) // hash(o))
```

    8740170526345
    139842728421520
    16

3，但 dict() 和 set() 不止需要 __hash__() 还需要 __eq__()
默认的 __eq__(self, other) 的实现是 self is other
换句话说就是比地址

```python
o = my_class()
p = my_class()
q = o
print(id(o))
print(id(p))
print(id(q))
print(o == p)
print(o == q)
```

    139842728415696
    139842728415632
    139842728415696
    False
    True

如果只定义 eq (和ne)， hash 会消失 （原因不明）

```python
class my_class(object): 
    def __eq__(self, other):
        return True
    def __ne__(self, other):
        return False
    
o = my_class()
hash(o)
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-11-e7958ecab408> in <module>
          6 
          7 o = my_class()
    ----> 8 hash(o)
    

    TypeError: unhashable type: 'my_class'

但是可以只定义 hash ， eq 还是默认的

```python
class my_class(object): 
    def __hash__(self):
        return 1
    
o = my_class()
p = my_class()
q = o
print(id(o))
print(id(p))
print(id(q))
print(o == p)
print(o == q)
{o, p, q}
```

    139842728468688
    139842728468752
    139842728468688
    False
    True





    {<__main__.my_class at 0x7f2fac27a0d0>, <__main__.my_class at 0x7f2fac27a110>}


如果 hashable 就可以放进 set 或者用作 dict 的 key。
但是要实现没有重复，必须实现有意义的 eq 才行
上面这个例子就是没有意义的
== 检测相等的 o q 只留下来一个，p 也留下来了，所以有两个.
即使 hash 值相同也没有问题，只是一般的 hash table collision 而已。
只有性能的影响，不会报错。

```python
# sane example
class my_class(object): 
    def __init__(self, v):
        self.v = v
    def __repr__(self):
        return str(self.v) + '@' + str(id(self))
    def __hash__(self):
        return 1
    def __eq__(self, other):
        return self.v == other.v
    
o = my_class(1)
p = my_class(2)
q = o
r = my_class(2)
print(id(o))
print(id(p))
print(id(q))
print(id(r))
print(o == p)
print(o == q)
print(o == r)
{o, p, q, r}
```

    139842763899344
    139842763900368
    139842763899344
    139842763899664
    False
    True
    False





    {1@139842763899344, 2@139842763900368}




```python
# insane example
class my_class(object): 
    def __init__(self, v):
        self.v = v
    def __repr__(self):
        return str(self.v) + '@' + str(id(self))
    def __hash__(self):
        return 1
    def __eq__(self, other):
        return self.v != other.v
    
o = my_class(1)
p = my_class(2)
q = o
r = my_class(2)
print(id(o))
print(id(p))
print(id(q))
print(id(r))
print(o == p)
print(o == q)
print(o == r)
{o, p, q, r}
```

    139842728418448
    139842728418192
    139842728418448
    139842728418320
    True
    False
    True





    {1@139842728418448}


上面的例子表明
eq 表示相等的变量不会重复出现
即使 eq 定义的非常出格，系统也不会在 set() 里保存两份同样地址的变量。4，如果你非要把 list 放进 set，只需要定义它的 hash 函数就好了

```python
class my_list(list):
    def __hash__(self):
        return id(self)//16
    
a = list([1, 2, 3])
b = my_list([4, 5, 6])
a.append(7)
b.append(8) # warking in the same way
```


```python
{a}
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-16-29dfa031a339> in <module>
    ----> 1 {a}
    

    TypeError: unhashable type: 'list'



```python
{b}
```




    {[4, 5, 6, 8]}




```python

```
