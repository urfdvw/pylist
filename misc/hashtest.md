# Test the behaviour when put an object into a set

First we define a class.
```python
class myclass:
    def __init__(self, val):
        self.val = val
    def set_val(self, val):
        self.val = val
```
We see the object of this class is hashable
```python
a = myclass(0)
print(a.__hash__())
```
```
8343402272183
```
In place operation does not change the hash value.
I guess it is because the reference did not change.
```python
a.set_val(2)
print(a.__hash__())
```
```
8343402272183
```
Different object will have different hash value even though the data are exactly the same
```python
b = myclass(0)
print(b.__hash__())
```
```
8343402264626
```
But name changing does not change hash value
```python
c = b
print(c.__hash__())
```
```
8343402264626
```
So we know, when we store a object in a set, we can understand what is happening.
```python
myset = set()
myset.add(a)
myset.add(b)
myset.add(c)
print(len(myset))

print(a in myset)
print(b in myset)
print(c in myset)
c.set_val(5)
print(c in myset)
print(myclass(0) in myset)
```
```
2
True
True
True
True
False
```