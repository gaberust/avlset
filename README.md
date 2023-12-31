# avlset

![GitHub repo size](https://img.shields.io/github/repo-size/gaberust/avlset?style=flat-square)
![GitHub contributors](https://img.shields.io/github/contributors/gaberust/avlset?style=flat-square)
![GitHub stars](https://img.shields.io/github/stars/gaberust/avlset?style=flat-square)
![GitHub forks](https://img.shields.io/github/forks/gaberust/avlset?style=flat-square)
![PyPI](https://img.shields.io/pypi/dm/avlset?style=flat-square)

avlset is a Python package that provides a self-sorting, non-duplicating data structure using a custom AVL Tree 
implementation. The AVL Tree is a binary search tree with automatic tree balancing. The `AVLSet` object allows users 
to insert data with confidence that it will be returned sorted and unique. avlset also provides basic type hinting 
support in addition to support for multiple built-in Python operators.

## Prerequisites

The avlset package requires Python 3.6+.

## Installing avlset

avlset is nearly written using raw Python, except for pulling in the built-in typing module for type-hinting support in 
less modern Python versions. Downloading [avlset.py](./avlset/avlset.py) and placing it in your project directory is 
to use. Alternatively, it can be installed from PyPI using pip:
```bash
pip install avlset
```

## Using avlset

```python
from avlset import AVLSet

# Create an instance of AVLSet. The type hint is optional, but recommended.
# Data must be comparable using <, =, and >.
# Using mismatched data types in the same set *will* cause issues.
# This will also work with more complex types like lists ans tuples, if the columns match.
# For example, (str, int) and (str, int) will compare just fine, but (str, str) and (str, int) will break everything.
# Using proper type hinting will help prevent this in larger applications.
myset: AVLSet[int] = AVLSet()

test_data = [3, 5, 2, 7, 2, 4, 2, 6, 2, 8, 7, 10]

# Insert data into set
for n in test_data:
    myset.insert(n)
print(list(myset))  # [2, 3, 4, 5, 6, 7, 8, 10]

# Remove specific data from set
myset.remove(6)
print(list(myset))  # [2, 3, 4, 5, 7, 8, 10]

# Remove and retrieve first (min) item in set
print(myset.pop())  # 2  # OR myset.pop_min()
print(list(myset))  # [3, 4, 5, 7, 8, 10]

# Remove and retrieve last (max) item in set
print(myset.pop_max())  # 10
print(list(myset))  # [3, 4, 5, 7, 8]

# Iterating through set, ascending and descending
for n in myset:
    print(n)
for n in reversed(myset):
    print(n)

# Checking if items exist in set
print(4 in myset)  # True
print(4 not in myset)  # False
print(17 in myset)  # False
print(17 not in myset)  # True

# AVLSet is falsy when empty, and truthy when not
print(bool(myset))  # True
while myset:  # Breaks when list is empty
    myset.pop()
print(bool(myset))  # False
```