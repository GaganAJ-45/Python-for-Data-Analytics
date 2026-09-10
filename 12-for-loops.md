# For Loops in Python

## 1. What is a For Loop?

A `for` loop iterates over a **sequence** (list, string, tuple, dict, set, range) and executes a block of code for each element.

```
For each item in sequence → run block → next item → run block → ...until end
```

**Where to use:**
- When you know the number of iterations in advance
- Iterating over lists, strings, tuples, dicts, sets
- Running code N times using `range()`
- Traversing arrays in DSA problems

---

## 2. Basic Syntax

```python
for variable in iterable:
    # body — runs for each item
```

```python
# Iterate over a list
fruits = ["apple", "banana", "cherry"]
for fruit in fruits:
    print(fruit)
# Output:
# apple
# banana
# cherry

# Iterate over a string
for char in "Python":
    print(char, end=" ")
# Output: P y t h o n

# Iterate over a range
for i in range(5):
    print(i, end=" ")
# Output: 0 1 2 3 4
```

---

## 3. `range()` — Generate a Sequence of Numbers

`range(start, stop, step)` generates numbers in a given range.

| Usage | Output |
|---|---|
| `range(5)` | 0, 1, 2, 3, 4 |
| `range(1, 6)` | 1, 2, 3, 4, 5 |
| `range(1, 10, 2)` | 1, 3, 5, 7, 9 |
| `range(10, 0, -1)` | 10, 9, 8, ... 1 |
| `range(0, 11, 2)` | 0, 2, 4, 6, 8, 10 |

```python
# Print 1 to 10
for i in range(1, 11):
    print(i, end=" ")
# Output: 1 2 3 4 5 6 7 8 9 10

# Print even numbers 2 to 20
for i in range(2, 21, 2):
    print(i, end=" ")
# Output: 2 4 6 8 10 12 14 16 18 20

# Countdown
for i in range(5, 0, -1):
    print(i, end=" ")
print("Go!")
# Output: 5 4 3 2 1 Go!

# range() is lazy — doesn't store all values in memory
r = range(1, 1000000)
print(type(r))   # Output: <class 'range'>
print(list(r[:5]))  # Output: [1, 2, 3, 4, 5]
```

> **Interview tip:** `range()` is a lazy object — it generates numbers on demand without storing them all in memory. This is why `range(1000000)` is memory efficient — it uses the same amount of memory as `range(5)`.

---

## 4. `break` and `continue` in For Loops

### `break` — exit loop early
```python
# Find first even number
numbers = [1, 3, 5, 4, 7, 9]
for num in numbers:
    if num % 2 == 0:
        print(f"First even: {num}")
        break
# Output: First even: 4
```

### `continue` — skip current iteration
```python
# Print only odd numbers
for i in range(1, 11):
    if i % 2 == 0:
        continue
    print(i, end=" ")
# Output: 1 3 5 7 9
```

### `pass` — placeholder
```python
for i in range(5):
    pass   # TODO: implement later
```

---

## 5. `for-else`

The `else` block runs **only if the loop completed without a `break`**.

```python
# Search for target
numbers = [10, 20, 30, 40, 50]
target  = 35

for num in numbers:
    if num == target:
        print(f"Found {target}!")
        break
else:
    print(f"{target} not found")
# Output: 35 not found

# Prime check — clean using for-else
num = 29
for i in range(2, int(num**0.5) + 1):
    if num % i == 0:
        print("Not prime")
        break
else:
    print("Prime")   # no break occurred — prime confirmed
# Output: Prime
```

> **Interview tip:** `for-else` is unique to Python. The `else` is associated with the loop, not an `if`. It runs when the loop exhausts the iterable without hitting `break`. This is the cleanest way to write search-and-confirm patterns.

---

## 6. `enumerate()` — Index + Value Together

`enumerate()` gives both the **index** and the **value** while iterating.

```python
fruits = ["apple", "banana", "cherry"]

# Without enumerate — ugly
for i in range(len(fruits)):
    print(i, fruits[i])

# With enumerate — clean ✅
for i, fruit in enumerate(fruits):
    print(i, fruit)
# 0 apple
# 1 banana
# 2 cherry

# Start index from 1
for i, fruit in enumerate(fruits, start=1):
    print(f"{i}. {fruit}")
# 1. apple
# 2. banana
# 3. cherry
```

> **Interview tip:** Never use `range(len(lst))` when you need both index and value. Use `enumerate()` — it is more Pythonic and readable.

---

## 7. `zip()` — Iterate Multiple Lists Together

`zip()` pairs elements from multiple iterables.

```python
names  = ["AJ", "Rahul", "Priya"]
scores = [95, 87, 92]
grades = ["A", "B", "A"]

for name, score, grade in zip(names, scores, grades):
    print(f"{name}: {score} ({grade})")
# AJ: 95 (A)
# Rahul: 87 (B)
# Priya: 92 (A)

# zip stops at the shortest iterable
a = [1, 2, 3, 4]
b = ["a", "b"]
print(list(zip(a, b)))   # Output: [(1, 'a'), (2, 'b')]

# Create dict from two lists
keys   = ["name", "age", "city"]
values = ["AJ", 22, "Bengaluru"]
d = dict(zip(keys, values))
print(d)   # Output: {'name': 'AJ', 'age': 22, 'city': 'Bengaluru'}
```

---

## 8. Iterating Over Different Data Structures

### List
```python
numbers = [10, 20, 30]
for num in numbers:
    print(num)
```

### String — character by character
```python
for char in "Python":
    print(char)
```

### Tuple
```python
coords = (10, 20, 30)
for c in coords:
    print(c)
```

### Dictionary — 4 ways
```python
d = {"name": "AJ", "age": 22}

for key in d:                    # keys (default)
    print(key)

for key in d.keys():             # keys explicit
    print(key)

for value in d.values():         # values
    print(value)

for key, value in d.items():     # key-value pairs
    print(f"{key}: {value}")
```

### Set
```python
fruits = {"apple", "banana", "cherry"}
for fruit in fruits:
    print(fruit)
# order not guaranteed — sets are unordered
```

---

## 9. Nested For Loops

A loop inside a loop — outer loop runs once, inner loop runs completely.

```python
# Multiplication table
for i in range(1, 4):
    for j in range(1, 4):
        print(f"{i} x {j} = {i*j}")
    print()   # blank line after each row

# Pattern — right triangle
n = 5
for row in range(1, n + 1):
    for col in range(row):
        print("*", end=" ")
    print()
# *
# * *
# * * *
# * * * *
# * * * * *
```

> **Interview tip:** Nested loops are O(n²) — always mention this when analyzing time complexity. A common interview question is to optimize an O(n²) nested loop solution to O(n) using a dict or set.

---

## 10. List Comprehension — Compact For Loop

Create a list using a one-line for loop.

```python
# Regular for loop
squares = []
for x in range(6):
    squares.append(x**2)

# List comprehension — same result
squares = [x**2 for x in range(6)]
print(squares)   # Output: [0, 1, 4, 9, 16, 25]

# With condition
evens = [x for x in range(10) if x % 2 == 0]
print(evens)     # Output: [0, 2, 4, 6, 8]

# Nested comprehension — flatten matrix
matrix = [[1,2,3],[4,5,6],[7,8,9]]
flat   = [num for row in matrix for num in row]
print(flat)      # Output: [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

### Dict Comprehension
```python
squares = {x: x**2 for x in range(1, 6)}
print(squares)   # Output: {1: 1, 2: 4, 3: 9, 4: 16, 5: 25}
```

### Set Comprehension
```python
unique_squares = {x**2 for x in [-2, -1, 0, 1, 2]}
print(unique_squares)   # Output: {0, 1, 4}
```

---

## 11. DSA Patterns Using For Loops

### Array Traversal
```python
arr = [10, 20, 30, 40, 50]

# By value
for num in arr:
    print(num)

# By index — when you need position
for i in range(len(arr)):
    print(f"arr[{i}] = {arr[i]}")

# Both — enumerate
for i, num in enumerate(arr):
    print(f"arr[{i}] = {num}")
```

### Find Maximum — O(n)
```python
arr = [50, 25, 7, 60, 15]
maximum = arr[0]   # initialize with first element NOT 0

for num in arr:
    if num > maximum:
        maximum = num

print(maximum)   # Output: 60
```

### Linear Search — O(n)
```python
def linear_search(arr, target):
    for i, num in enumerate(arr):
        if num == target:
            return i
    return -1

arr = [10, 25, 7, 60, 15]
print(linear_search(arr, 60))   # Output: 3
print(linear_search(arr, 99))   # Output: -1
```

### Count Frequency — O(n)
```python
arr  = [1, 2, 3, 1, 2, 1]
freq = {}
for num in arr:
    freq[num] = freq.get(num, 0) + 1
print(freq)   # Output: {1: 3, 2: 2, 3: 1}
```

### Two Sum — Brute Force O(n²)
```python
def two_sum(arr, target):
    for i in range(len(arr)):
        for j in range(i + 1, len(arr)):
            if arr[i] + arr[j] == target:
                return [i, j]
    return []

print(two_sum([2, 7, 4, 3], 10))   # Output: [1, 2]
```

### Prefix Sum — O(n) preprocessing
```python
arr    = [1, 2, 3, 4, 5]
prefix = [0] * len(arr)
prefix[0] = arr[0]

for i in range(1, len(arr)):
    prefix[i] = prefix[i-1] + arr[i]

print(prefix)   # Output: [1, 3, 6, 10, 15]
# Now range sum query is O(1): sum(i,j) = prefix[j] - prefix[i-1]
```

---

## 12. `for` vs `while` — Quick Comparison

| | `for` | `while` |
|---|---|---|
| Use when | Iterating over sequence / known count | Condition-based / unknown count |
| Sequence needed | ✅ Yes | ❌ No |
| Infinite loop | Harder | Easy (`while True`) |
| Counter needed | Not always | Usually yes |
| DSA use | Array traversal, frequency count | Binary search, two pointer |

---

## Quick Reference

```python
# BASIC
for item in iterable:
    body

# RANGE
range(n)            # 0 to n-1
range(a, b)         # a to b-1
range(a, b, step)   # a to b-1 with step
range(n, 0, -1)     # countdown

# ENUMERATE
for i, val in enumerate(lst):
for i, val in enumerate(lst, start=1):

# ZIP
for a, b in zip(lst1, lst2):

# BREAK / CONTINUE / PASS
for item in lst:
    if condition: break     # exit loop
    if condition: continue  # skip iteration
    if condition: pass      # do nothing

# FOR-ELSE
for item in lst:
    if found: break
else:
    not_found_code          # runs if no break

# COMPREHENSIONS
[expr for x in lst]                    # list
[expr for x in lst if condition]       # filtered list
{k: v for k, v in items}              # dict
{expr for x in lst}                   # set

# DICT ITERATION
for k in d:                # keys
for k in d.keys():         # keys
for v in d.values():       # values
for k, v in d.items():     # key-value
```

---

## Interview Short Answers

**Q: What is the difference between `for` and `while` loops?**
> A `for` loop iterates over a sequence or a known number of times using `range()`. A `while` loop runs as long as a condition is True — used when the number of iterations is unknown. In DSA, `for` is used for array traversal and frequency counting, while `while` is used for binary search and two-pointer techniques.

**Q: What is `range()` and is it memory efficient?**
> `range()` generates a sequence of numbers based on start, stop, and step parameters. It is a lazy object — it does not store all the numbers in memory at once. It generates each number on demand, which is why `range(1000000)` uses the same memory as `range(5)`. This makes it extremely memory efficient for large ranges.

**Q: What is the difference between iterating with `range(len(lst))` vs directly iterating?**
> Direct iteration `for item in lst` is cleaner and more Pythonic — use it when you only need the value. `range(len(lst))` gives you the index — use it when you need the position. When you need both, use `enumerate(lst)` which is the most Pythonic approach and avoids the verbose `range(len())`.

**Q: What is `for-else` in Python?**
> The `else` block of a `for` loop executes only when the loop completes without hitting a `break`. It is commonly used in search algorithms — if the loop exhausts all elements without finding the target, the `else` block handles the not-found case. This is unique to Python and not found in most other languages.

**Q: What is a list comprehension and why use it?**
> A list comprehension is a concise way to create a list using a `for` loop in a single line: `[expression for item in iterable if condition]`. It is more readable and typically 30-50% faster than an equivalent `for` loop with `append()` because it is optimized internally by Python. It also works for dict and set comprehensions.

**Q: What is the time complexity of a nested for loop?**
> A nested for loop where both loops iterate n times has O(n²) time complexity — the inner loop runs n times for each of the n outer iterations. A common interview pattern is to optimize an O(n²) brute-force nested loop to O(n) using a hash map or set for lookups instead of the inner loop.
