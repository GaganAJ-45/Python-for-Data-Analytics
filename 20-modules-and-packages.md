# Modules and Packages in Python
> Foundation Notes — Interview Ready | DSA Focused

---

## 1. What is a Module?

A **module** is simply a Python file (`.py`) that contains functions, classes, and variables you can reuse in other programs.

```
my_math.py        ← this is a module
main.py           ← imports and uses my_math
```

**Why modules?**
- Avoid rewriting the same code in every file
- Organize code into logical units
- Share code across projects
- Python's standard library is a collection of built-in modules

---

## 2. Importing Modules

### `import module` — import the whole module
```python
import math

print(math.pi)          # Output: 3.141592653589793
print(math.sqrt(16))    # Output: 4.0
print(math.floor(3.7))  # Output: 3
print(math.ceil(3.2))   # Output: 4
```

### `from module import name` — import specific items
```python
from math import pi, sqrt, floor

print(pi)        # Output: 3.141592653589793
print(sqrt(25))  # Output: 5.0  — no need for math.sqrt
```

### `import module as alias` — give it a short name
```python
import numpy as np          # industry standard alias
import pandas as pd         # industry standard alias
import matplotlib.pyplot as plt
```

### `from module import *` — import everything (avoid this)
```python
from math import *    # ❌ bad practice — pollutes namespace
print(sqrt(9))        # works but unclear where sqrt came from
```

> **Interview tip:** Avoid `import *` — it makes code hard to read and can cause name conflicts. Always use explicit imports.

---

## 3. Creating Your Own Module

**Step 1 — Create `my_utils.py`:**
```python
# my_utils.py

PI = 3.14159

def add(a, b):
    return a + b

def multiply(a, b):
    return a * b

def is_even(n):
    return n % 2 == 0

class Calculator:
    def square(self, n):
        return n ** 2
```

**Step 2 — Import and use in `main.py`:**
```python
# main.py
import my_utils

print(my_utils.PI)              # Output: 3.14159
print(my_utils.add(3, 4))       # Output: 7
print(my_utils.is_even(10))     # Output: True

calc = my_utils.Calculator()
print(calc.square(5))           # Output: 25
```

**Or import specific items:**
```python
from my_utils import add, is_even, PI

print(add(3, 4))      # Output: 7
print(PI)             # Output: 3.14159
```

---

## 4. `if __name__ == "__main__"`

Every Python file has a built-in variable `__name__`.
- When a file runs directly: `__name__ == "__main__"`
- When a file is imported: `__name__ == "filename"`

```python
# my_utils.py

def add(a, b):
    return a + b

def is_even(n):
    return n % 2 == 0

# This block only runs when THIS file is run directly
# It does NOT run when imported by another file
if __name__ == "__main__":
    print("Testing my_utils:")
    print(add(3, 4))     # Output: 7
    print(is_even(5))    # Output: False
```

```python
# main.py
import my_utils
# The if __name__ == "__main__" block in my_utils does NOT run
result = my_utils.add(10, 20)
print(result)   # Output: 30
```

> **Interview tip:** `if __name__ == "__main__"` is essential Python. It lets a file be both a reusable module AND a runnable script. Always use it to separate module code from test/demo code.

---

## 5. What is a Package?

A **package** is a folder containing multiple modules, with a special `__init__.py` file that marks it as a package.

```
my_package/
    __init__.py        ← marks this folder as a package
    math_utils.py
    string_utils.py
    file_utils.py
```

```python
# Importing from a package
import my_package.math_utils
from my_package import string_utils
from my_package.file_utils import read_file
```

### `__init__.py`
```python
# my_package/__init__.py
# Can be empty, or can expose selected items:

from .math_utils import add, multiply
from .string_utils import reverse_string

# Now users can do:
# from my_package import add
# instead of:
# from my_package.math_utils import add
```

---

## 6. Standard Library — Built-in Modules

Python ships with a rich standard library — no installation needed.

### `math` — mathematical operations
```python
import math

math.pi          # 3.14159...
math.e           # 2.71828...
math.sqrt(16)    # 4.0
math.pow(2, 10)  # 1024.0
math.floor(3.9)  # 3
math.ceil(3.1)   # 4
math.log(100, 10)  # 2.0  — log base 10
math.factorial(5)  # 120
math.gcd(48, 18)   # 6
math.inf         # infinity
```

### `random` — random number generation
```python
import random

random.random()              # float between 0.0 and 1.0
random.randint(1, 10)        # int between 1 and 10 inclusive
random.choice([1, 2, 3, 4])  # random item from list
random.choices([1,2,3], k=3) # 3 items with replacement
random.sample([1,2,3,4,5], 3) # 3 unique items
random.shuffle([1, 2, 3, 4]) # shuffle list in place
random.seed(42)              # for reproducible results
```

### `os` — operating system interface
```python
import os

os.getcwd()                        # current directory
os.listdir(".")                    # files in directory
os.path.exists("file.txt")         # check existence
os.path.join("folder", "file.txt") # join paths
os.makedirs("new_dir", exist_ok=True)
os.environ["HOME"]                 # environment variables
os.getenv("PATH", "/usr/bin")      # with default
```

### `sys` — system-specific parameters
```python
import sys

sys.argv          # command line arguments list
sys.path          # list of directories Python searches for modules
sys.version       # Python version string
sys.platform      # 'win32', 'linux', 'darwin'
sys.exit(0)       # exit program (0 = success)
sys.getrecursionlimit()  # 1000 default
sys.maxsize       # max int size
```

### `datetime` — date and time
```python
from datetime import datetime, date, timedelta

# Current date and time
now = datetime.now()
print(now)                           # 2025-07-01 14:30:00.123456

# Current date only
today = date.today()
print(today)                         # 2025-07-01

# Create specific date
d = date(2025, 1, 26)
print(d.strftime("%d %B %Y"))        # 26 January 2025

# Date arithmetic
tomorrow = today + timedelta(days=1)
last_week = today - timedelta(weeks=1)

# Format datetime
print(now.strftime("%Y-%m-%d %H:%M:%S"))  # 2025-07-01 14:30:00

# Parse string to datetime
dt = datetime.strptime("2025-01-26", "%Y-%m-%d")
```

### `collections` — specialized container types
```python
from collections import Counter, defaultdict, deque, namedtuple

# Counter — count occurrences
words = ["apple", "banana", "apple", "cherry", "banana", "apple"]
count = Counter(words)
print(count)                    # Counter({'apple': 3, 'banana': 2, 'cherry': 1})
print(count.most_common(2))     # [('apple', 3), ('banana', 2)]

# defaultdict — dict with default value for missing keys
dd = defaultdict(list)
dd["fruits"].append("apple")    # no KeyError — creates empty list automatically
dd["fruits"].append("banana")
print(dd)                       # defaultdict(<class 'list'>, {'fruits': ['apple', 'banana']})

# deque — double-ended queue (O(1) append/pop from both ends)
dq = deque([1, 2, 3])
dq.appendleft(0)    # [0, 1, 2, 3]
dq.append(4)        # [0, 1, 2, 3, 4]
dq.popleft()        # removes 0
dq.pop()            # removes 4

# namedtuple — tuple with named fields
Point = namedtuple("Point", ["x", "y"])
p = Point(3, 4)
print(p.x, p.y)     # Output: 3 4
print(p[0], p[1])   # Output: 3 4  — also works like regular tuple
```

### `itertools` — efficient iterators
```python
import itertools

# combinations — no repeats, order doesn't matter
list(itertools.combinations([1, 2, 3], 2))
# [(1, 2), (1, 3), (2, 3)]

# permutations — all orderings
list(itertools.permutations([1, 2, 3], 2))
# [(1, 2), (1, 3), (2, 1), (2, 3), (3, 1), (3, 2)]

# product — cartesian product
list(itertools.product([1, 2], ["a", "b"]))
# [(1, 'a'), (1, 'b'), (2, 'a'), (2, 'b')]

# chain — concatenate iterables
list(itertools.chain([1, 2], [3, 4], [5]))
# [1, 2, 3, 4, 5]

# accumulate — running total
list(itertools.accumulate([1, 2, 3, 4, 5]))
# [1, 3, 6, 10, 15]
```

### `functools` — higher-order functions
```python
from functools import reduce, lru_cache, partial

# reduce — apply function cumulatively
from functools import reduce
result = reduce(lambda x, y: x + y, [1, 2, 3, 4, 5])
print(result)   # Output: 15

# lru_cache — memoization
@lru_cache(maxsize=None)
def fib(n):
    if n <= 1: return n
    return fib(n-1) + fib(n-2)

# partial — fix some arguments
def power(base, exp):
    return base ** exp

square = partial(power, exp=2)
cube   = partial(power, exp=3)
print(square(5))   # Output: 25
print(cube(3))     # Output: 27
```

### `string` — string constants
```python
import string

print(string.ascii_letters)   # abcdefghijklmnopqrstuvwxyzABCDEF...
print(string.ascii_lowercase) # abcdefghijklmnopqrstuvwxyz
print(string.ascii_uppercase) # ABCDEFGHIJKLMNOPQRSTUVWXYZ
print(string.digits)          # 0123456789
print(string.punctuation)     # !"#$%&'()*+,-./:;<=>?@[\]^_`{|}~
```

---

## 7. `pip` — Installing Third-Party Packages

```bash
# Install a package
pip install requests
pip install pandas
pip install numpy

# Install specific version
pip install requests==2.28.0

# Install from requirements file
pip install -r requirements.txt

# Upgrade a package
pip install --upgrade requests

# Uninstall
pip uninstall requests

# List installed packages
pip list

# Show info about a package
pip show requests

# Save installed packages to file
pip freeze > requirements.txt
```

### `requirements.txt`
```
pandas==2.0.0
numpy==1.24.0
requests==2.28.2
matplotlib==3.7.0
```

---

## 8. Virtual Environments

A virtual environment isolates project dependencies so different projects can use different package versions.

```bash
# Create virtual environment
python -m venv myenv

# Activate (Linux/Mac)
source myenv/bin/activate

# Activate (Windows)
myenv\Scripts\activate

# Install packages (now isolated to this project)
pip install pandas numpy

# Deactivate
deactivate
```

> **Interview tip:** Always use virtual environments for projects. It shows professional development practice. Mention this when asked about project setup.

---

## 9. Useful Third-Party Packages for Your Roles

| Package | Use | Install |
|---|---|---|
| `pandas` | Data manipulation, DataFrames | `pip install pandas` |
| `numpy` | Numerical computing, arrays | `pip install numpy` |
| `matplotlib` | Data visualization, charts | `pip install matplotlib` |
| `requests` | HTTP calls, APIs | `pip install requests` |
| `sqlalchemy` | Database ORM | `pip install sqlalchemy` |
| `openpyxl` | Read/write Excel files | `pip install openpyxl` |
| `pytest` | Testing framework | `pip install pytest` |
| `flask` | Web framework (lightweight) | `pip install flask` |

---

## Quick Reference

```python
# IMPORTING
import module                    # import whole module
from module import name          # import specific item
from module import name as alias # import with alias
import module as alias           # module alias

# CHECKING MODULE
import math
print(dir(math))     # list all names in module
print(help(math))    # full documentation

# __name__ GUARD
if __name__ == "__main__":
    # runs only when file executed directly
    # NOT when imported

# STANDARD LIBRARY QUICK PICKS
import math          # sqrt, pi, floor, ceil, gcd, factorial
import random        # randint, choice, shuffle, seed
import os            # path, getcwd, listdir, makedirs
import sys           # argv, path, exit, version
import datetime      # now(), today(), timedelta, strftime
import json          # dump, load, dumps, loads
import csv           # reader, writer, DictReader, DictWriter
import re            # regex — search, match, findall, sub
import time          # sleep, time, perf_counter

from collections import Counter, defaultdict, deque, namedtuple
from functools   import reduce, lru_cache, partial
from itertools   import combinations, permutations, chain, product

# PIP
# pip install package
# pip freeze > requirements.txt
# pip install -r requirements.txt
```

---

## Interview Short Answers

**Q: What is the difference between a module and a package?**
> A module is a single Python file (`.py`) containing functions, classes, and variables that can be imported and reused. A package is a directory of modules with a special `__init__.py` file that marks the folder as a package. Packages allow organizing related modules together — for example, a `data_processing` package could have modules for reading, cleaning, and analyzing data.

**Q: What does `if __name__ == "__main__"` do?**
> Every Python file has a built-in `__name__` variable. When a file is run directly, `__name__` is set to `"__main__"`. When a file is imported as a module, `__name__` is set to the module's filename. This guard lets you write code that only runs when the file is executed directly — like tests or a main entry point — without that code running when the file is imported by another module.

**Q: What is the difference between `import math` and `from math import sqrt`?**
> `import math` imports the whole module — you access items with `math.sqrt()`. `from math import sqrt` imports only `sqrt` into the current namespace — you call it directly as `sqrt()`. The first approach is safer and avoids name conflicts. The second is convenient for frequently used items. Avoid `from math import *` as it imports everything and can cause naming collisions.

**Q: What is `pip` and what is `requirements.txt`?**
> `pip` is Python's package manager — it downloads and installs third-party packages from PyPI (Python Package Index). `requirements.txt` is a file listing all packages and their versions a project needs. Running `pip freeze > requirements.txt` captures the current environment, and `pip install -r requirements.txt` recreates it — essential for sharing projects and deployment.

**Q: What is a virtual environment and why use it?**
> A virtual environment is an isolated Python environment with its own installed packages, separate from the system Python. Without it, all projects share the same packages, causing version conflicts — Project A needs `pandas==1.5` while Project B needs `pandas==2.0`. Virtual environments solve this by giving each project its own isolated package set. Created with `python -m venv myenv` and activated before installing packages.

**Q: Name some useful standard library modules and what they do.**
> `math` for mathematical functions. `os` for file system and operating system operations. `sys` for system parameters like command-line arguments. `datetime` for dates, times, and time arithmetic. `json` for reading and writing JSON data. `csv` for CSV file handling. `collections` for specialized containers like `Counter`, `defaultdict`, and `deque`. `itertools` for efficient iteration tools. `functools` for higher-order functions like `lru_cache` and `partial`. None of these need installation — they ship with Python.

**Q: What is the `collections` module and name its most useful types?**
> The `collections` module provides specialized container types beyond the built-in list, dict, and tuple. `Counter` counts occurrences of elements and supports `most_common()`. `defaultdict` is a dict that auto-creates a default value for missing keys — no KeyError. `deque` is a double-ended queue with O(1) append and pop from both ends, used for BFS in graphs. `namedtuple` creates tuple subclasses with named fields for better readability.
