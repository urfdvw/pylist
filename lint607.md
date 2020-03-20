# [607. Two Sum III - Data structure design](https://www.lintcode.com/problem/two-sum-iii-data-structure-design/description)

Design and implement a TwoSum class. It should support the following operations: add and find.

- add - Add the number to an internal data structure.
- find - Find if there exists any pair of numbers which sum is equal to the value.

Example
```
add(1); add(3); add(5);
find(4) // return true
find(7) // return false
```
# solution
```python
class TwoSum:
    """
    use a dict to store data
        key is the number, value is the number of occurance
    """
    
    """
    @param number: An integer
    @return: nothing
    """
    
    def __init__(self):
        self.data = dict()
    
    def add(self, number):
        # key: number
        # value: counting of that number
        self.data.setdefault(number, 0)
        self.data[number] += 1

    """
    @param value: An integer
    @return: Find if there exists any pair of numbers which sum is equal to the value.
    """
    def find(self, value):
        for a, n_a in self.data.items():
            # a + b = value
            b = value - a  
            # if b is not found, no pair contains a exists
            if b not in self.data:
                continue
            # if exist, if different, then must exist
            if a != b:
                return True
            # if the same, check is there are enough counting of that number
            if n_a >= 2:
                return True
        # if not found through the for-loop
        return False
```

# special care
- Because value is not fixed, checking of existance of a key in dict is done in find function
- There can be a case that two numbers are the same, but only 1 counting, that means return False
- `high` and `low` are very bad naming of the variables. even `a` and `b` are better naming of the numbers