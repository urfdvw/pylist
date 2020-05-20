# Numpy Cheat Sheet
```python
import numpy as np
```

## Matrix operation

vector can be used as either row or col vectors, depending on the position of the vector. The result is vector if `v @ m` or `m @ v`.

```python
a = np.ones([3,5])
b = np.ones(5)
c = np.ones(3)
print(a @ b)
print(c @ a)
```
```
[5. 5. 5.]
[3. 3. 3. 3. 3.]
```

Another usage is `@` can be used for inner product

1 dimension example:
```python
x = np.arange(5)
w = np.ones(5) / 5
print(w @ x)
```
```
2.0
```

Multidimension example:
```python
N = 1000
x = np.random.rand(N, 3)
w = np.ones(N) / N
print(w @ x)
```
```
[0.50443393 0.50878136 0.49507543]
```

## Data concat

Combine a list of vectors into a 2d array
```python
data_list = [np.ones(5) for i in range(3)]
data = np.vstack(data_list)
print(data.shape)
```
```
(3, 5)
```

Combine a list of arrays into a 2d array, keeping datum size
```python
data_list = [np.ones([2, 5]) for i in range(3)]
data = np.vstack(data_list)
print(data.shape)
```
```
(6, 5)
```

Combine a list of short vectors into a long one
```python
data_list = [np.ones(2) for i in range(3)]
data = np.hstack(data_list)
print(data.shape)
```
```
(6,)
```

## inplace or not
- `a.sort()` is in-place
- `a.flatten()` is not in-place