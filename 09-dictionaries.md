# Dictionaries in Python
> Foundation Notes — Interview Ready | DSA Focused

---

## 1. What is a Dictionary?

A dictionary is a collection of **key-value pairs**. It is:
- **Ordered** — maintains insertion order (Python 3.7+)
- **Mutable** — can add, remove, and change items
- **Keys must be unique** — duplicate keys overwrite the previous value
- **Keys must be immutable** — strings, numbers, tuples are valid keys; lists are not
- **Values can be anything** — any data type, including lists or other dicts

```python
# Syntax
my_dict = {
    "key1": "value1",
    "key2": "value2"
}
```

> ⚠️ **Interview note:** Dictionaries were unordered before Python 3.7. From Python 3.7 onwards they maintain **insertion order**. Always clarify this in interviews.

---

## 2. Creating a Dictionary

```python
# Method 1 — curly braces
student = {
    "name": "AJ",
    "age": 22,
    "city": "Bengaluru"
}

# Method 2 — dict() constructor
student = dict(name="AJ", age=22, city="Bengaluru")

# Method 3 — from list of tuples
pairs   = [("name", "AJ"), ("age", 22)]
student = dict(pairs)

# Empty dictionary
empty = {}
empty = dict()

# Real-world example — Karnataka cities and famous dishes
karnataka_food = {
    "Bengaluru" : "Bisi Bele Bath",
    "Mysuru"    : "Mysore Pak",
    "Mangaluru" : "Neer Dosa",
    "Shivamogga": "Kadubu",
    "Hubballi"  : "Girmit"
}
```

---

## 3. Accessing Elements

### By Key — `dict[key]`
```python
print(karnataka_food["Mysuru"])    # Output: Mysore Pak

# ⚠️ KeyError if key doesn't exist
print(karnataka_food["Chennai"])   # ❌ KeyError: 'Chennai'
```

### `get(key, default)` — safe access, no error
```python
print(karnataka_food.get("Mangaluru"))              # Output: Neer Dosa
print(karnataka_food.get("Chennai"))                # Output: None
print(karnataka_food.get("Chennai", "Not Found"))   # Output: Not Found
```

> **Interview tip:** Always prefer `get()` over `dict[key]` in production code — it won't crash if the key is missing. Use `dict[key]` only when you are 100% sure the key exists.

### Checking if a Key Exists — `in` operator
```python
print("Mysuru" in karnataka_food)       # Output: True   — checks KEYS
print("Mysore Pak" in karnataka_food)   # Output: False  — NOT checking values

# To check values
print("Mysore Pak" in karnataka_food.values())   # Output: True
```

---

## 4. Adding and Updating Elements

```python
# Add new key-value pair
karnataka_food["Belagavi"] = "Kunda"
print(karnataka_food)

# Update existing key — overwrites the value
karnataka_food["Bengaluru"] = "Ragi Mudde"
print(karnataka_food["Bengaluru"])   # Output: Ragi Mudde

# Duplicate key — latest value wins
d = {"a": 1, "a": 2, "a": 3}
print(d)   # Output: {'a': 3}  — only last value kept
```

---

## 5. Removing Elements

**`pop(key)`** — removes key and **returns** its value. Raises `KeyError` if not found.
```python
removed = karnataka_food.pop("Mysuru")
print(removed)   # Output: Mysore Pak

# With default — no error if key missing
val = karnataka_food.pop("Chennai", "Not found")
print(val)   # Output: Not found
```

**`popitem()`** — removes and returns the **last inserted** key-value pair as a tuple.
```python
d = {"a": 1, "b": 2, "c": 3}
last = d.popitem()
print(last)   # Output: ('c', 3)
print(d)      # Output: {'a': 1, 'b': 2}
```

**`del dict[key]`** — removes a key. Raises `KeyError` if not found.
```python
del karnataka_food["Mangaluru"]
print(karnataka_food)

# Delete the entire dictionary
del karnataka_food
```

**`clear()`** — removes all items, dict remains as empty `{}`.
```python
d = {"a": 1, "b": 2}
d.clear()
print(d)   # Output: {}
```

---

## 6. Dictionary Methods

**`keys()`** — returns all keys as a view object
```python
d = {"name": "AJ", "age": 22, "city": "Bengaluru"}

print(d.keys())    # Output: dict_keys(['name', 'age', 'city'])

# Convert to list
print(list(d.keys()))   # Output: ['name', 'age', 'city']
```

**`values()`** — returns all values as a view object
```python
print(d.values())        # Output: dict_values(['AJ', 22, 'Bengaluru'])
print(list(d.values()))  # Output: ['AJ', 22, 'Bengaluru']
```

**`items()`** — returns key-value pairs as tuples
```python
print(d.items())
# Output: dict_items([('name', 'AJ'), ('age', 22), ('city', 'Bengaluru')])

print(list(d.items()))
# Output: [('name', 'AJ'), ('age', 22), ('city', 'Bengaluru')]
```

**`update()`** — merges another dict into this one (in-place)
```python
d1 = {"a": 1, "b": 2}
d2 = {"b": 99, "c": 3}   # "b" will overwrite

d1.update(d2)
print(d1)   # Output: {'a': 1, 'b': 99, 'c': 3}

# Update with keyword arguments
d1.update(d=4, e=5)
print(d1)   # Output: {'a': 1, 'b': 99, 'c': 3, 'd': 4, 'e': 5}
```

**`setdefault(key, default)`** — returns value if key exists, sets default if it doesn't
```python
d = {"name": "AJ"}

# Key exists — returns existing value, does NOT overwrite
print(d.setdefault("name", "Unknown"))    # Output: AJ

# Key doesn't exist — sets and returns default
print(d.setdefault("age", 22))            # Output: 22
print(d)                                  # Output: {'name': 'AJ', 'age': 22}

# Real use: building a frequency counter cleanly
words = ["apple", "banana", "apple", "cherry"]
freq  = {}
for word in words:
    freq.setdefault(word, 0)
    freq[word] += 1
print(freq)   # Output: {'apple': 2, 'banana': 1, 'cherry': 1}
```

**`copy()`** — shallow copy of the dictionary
```python
original = {"a": 1, "b": [1, 2]}
copy_d   = original.copy()
copy_d["a"] = 99
print(original["a"])   # Output: 1  — primitive unchanged

copy_d["b"].append(3)
print(original["b"])   # Output: [1, 2, 3]  — nested list still shared!
```

---

## 7. Iterating a Dictionary — 4 Ways

```python
d = {"name": "AJ", "age": 22, "city": "Bengaluru"}

# 1. Iterate keys (default behavior)
for key in d:
    print(key)
# name
# age
# city

# 2. Iterate keys explicitly
for key in d.keys():
    print(key)

# 3. Iterate values
for value in d.values():
    print(value)
# AJ
# 22
# Bengaluru

# 4. Iterate key-value pairs — MOST USEFUL
for key, value in d.items():
    print(f"{key}: {value}")
# name: AJ
# age: 22
# city: Bengaluru
```

> **Interview tip:** `for key, value in d.items()` is the most commonly used pattern. Always use this when you need both key and value.

---

## 8. Dictionary Comprehension

Create dictionaries in one line — same concept as list comprehension.

```python
# Syntax
new_dict = {key_expr: value_expr for item in iterable if condition}
```

```python
# Squares dictionary
squares = {x: x**2 for x in range(1, 6)}
print(squares)   # Output: {1: 1, 2: 4, 3: 9, 4: 16, 5: 25}

# Filter — only even squares
even_sq = {x: x**2 for x in range(1, 6) if x % 2 == 0}
print(even_sq)   # Output: {2: 4, 4: 16}

# Swap keys and values
original = {"a": 1, "b": 2, "c": 3}
swapped  = {v: k for k, v in original.items()}
print(swapped)   # Output: {1: 'a', 2: 'b', 3: 'c'}

# Word length dictionary
words    = ["apple", "banana", "kiwi"]
lengths  = {word: len(word) for word in words}
print(lengths)   # Output: {'apple': 5, 'banana': 6, 'kiwi': 4}

# From two lists using zip
keys   = ["name", "age", "city"]
values = ["AJ", 22, "Bengaluru"]
d = {k: v for k, v in zip(keys, values)}
print(d)   # Output: {'name': 'AJ', 'age': 22, 'city': 'Bengaluru'}
```

---

## 9. Nested Dictionaries

Dictionaries inside dictionaries — represents real-world structured data.

```python
students = {
    "S001": {
        "name": "AJ",
        "age" : 22,
        "marks": [85, 90, 78]
    },
    "S002": {
        "name": "Rahul",
        "age" : 21,
        "marks": [70, 88, 92]
    }
}

# Access nested values
print(students["S001"]["name"])        # Output: AJ
print(students["S002"]["marks"][1])    # Output: 88

# Iterate nested dict
for roll, info in students.items():
    print(f"Roll: {roll}, Name: {info['name']}, Age: {info['age']}")

# Add new student
students["S003"] = {"name": "Priya", "age": 20, "marks": [95, 88, 91]}

# Safe access with get() on nested dict
city = students.get("S001", {}).get("city", "Not Available")
print(city)   # Output: Not Available
```

---

## 10. Merging Dictionaries

```python
d1 = {"a": 1, "b": 2}
d2 = {"b": 99, "c": 3}

# Method 1 — update() — in-place, modifies d1
d1.update(d2)
print(d1)        # Output: {'a': 1, 'b': 99, 'c': 3}

# Method 2 — unpacking — creates new dict (Python 3.5+)
merged = {**d1, **d2}
print(merged)    # Output: {'a': 1, 'b': 99, 'c': 3}
# later dict wins for duplicate keys

# Method 3 — | operator — creates new dict (Python 3.9+)
merged = d1 | d2
print(merged)

# Method 4 — |= operator — in-place (Python 3.9+)
d1 |= d2
```

> **Which to use?** `{**d1, **d2}` works from Python 3.5+ so it's the safest. `d1 | d2` is cleanest but requires Python 3.9+.

---

## 11. `collections.defaultdict`

Like a regular dict but provides a **default value** for missing keys instead of raising `KeyError`.

```python
from collections import defaultdict

# Default value is 0 for int
freq = defaultdict(int)
words = ["apple", "banana", "apple", "cherry", "banana", "apple"]

for word in words:
    freq[word] += 1    # no KeyError even first time

print(dict(freq))   # Output: {'apple': 3, 'banana': 2, 'cherry': 1}

# Default value is list
graph = defaultdict(list)
graph["A"].append("B")   # no need to initialize graph["A"] = []
graph["A"].append("C")
graph["B"].append("D")
print(dict(graph))   # Output: {'A': ['B', 'C'], 'B': ['D']}
```

> **DSA use:** `defaultdict(list)` is the standard way to build an adjacency list for graph problems.

---

## 12. `collections.Counter`

Counts the frequency of elements — returns a dict subclass.

```python
from collections import Counter

# Count characters in a string
text  = "banana"
count = Counter(text)
print(count)         # Output: Counter({'a': 3, 'n': 2, 'b': 1})

# Count words
words = ["apple", "banana", "apple", "cherry", "banana", "apple"]
count = Counter(words)
print(count)         # Output: Counter({'apple': 3, 'banana': 2, 'cherry': 1})

# Most common elements
print(count.most_common(2))   # Output: [('apple', 3), ('banana', 2)]

# Access like a dict
print(count["apple"])    # Output: 3
print(count["mango"])    # Output: 0  — no KeyError for missing keys

# Arithmetic on Counters
c1 = Counter("aab")
c2 = Counter("abb")
print(c1 + c2)   # Output: Counter({'b': 3, 'a': 3})
print(c1 - c2)   # Output: Counter({'a': 1})
```

> **DSA use:** `Counter` is used for anagram checks, frequency analysis, top-K elements. Know it well.

---

## 13. DSA Patterns Using Dictionaries

### Frequency Counter — most common pattern
```python
# Check if two strings are anagrams
def is_anagram(s1, s2):
    return Counter(s1) == Counter(s2)

print(is_anagram("listen", "silent"))   # Output: True
print(is_anagram("hello", "world"))     # Output: False
```

### Two Sum — O(n) using dict
```python
def two_sum(arr, target):
    seen = {}
    for i, num in enumerate(arr):
        complement = target - num
        if complement in seen:
            return [seen[complement], i]
        seen[num] = i
    return []

print(two_sum([2, 7, 4, 3], 10))   # Output: [1, 2]  (7+3=10)
```

### Group Anagrams
```python
from collections import defaultdict

def group_anagrams(words):
    groups = defaultdict(list)
    for word in words:
        key = tuple(sorted(word))   # sorted letters as tuple key
        groups[key].append(word)
    return list(groups.values())

words = ["eat", "tea", "tan", "ate", "nat", "bat"]
print(group_anagrams(words))
# Output: [['eat', 'tea', 'ate'], ['tan', 'nat'], ['bat']]
```

### Word Frequency
```python
text  = "the cat sat on the mat the cat"
freq  = {}
for word in text.split():
    freq[word] = freq.get(word, 0) + 1

# Sort by frequency
sorted_freq = sorted(freq.items(), key=lambda x: x[1], reverse=True)
print(sorted_freq)
# Output: [('the', 3), ('cat', 2), ('sat', 1), ('on', 1), ('mat', 1)]
```

---

## 14. Time Complexity — Must Know

| Operation | Average | Worst Case |
|---|---|---|
| Access `d[key]` | O(1) | O(n) |
| Insert / Update | O(1) | O(n) |
| Delete `del d[key]` | O(1) | O(n) |
| Search `key in d` | O(1) | O(n) |
| Iteration | O(n) | O(n) |
| `get()` | O(1) | O(n) |

> Worst case O(n) happens only when there are many hash collisions — extremely rare in practice. For interview purposes, all dict operations are **O(1)**.

---

## 15. List vs Tuple vs Set vs Dict — Full Comparison

| Feature | List | Tuple | Set | Dict |
|---|---|---|---|---|
| Ordered | ✅ | ✅ | ❌ | ✅ (3.7+) |
| Mutable | ✅ | ❌ | ✅ | ✅ |
| Duplicates | ✅ | ✅ | ❌ | Keys: ❌ |
| Indexed | ✅ | ✅ | ❌ | By key |
| Hashable | ❌ | ✅ | ❌ | ❌ |
| `in` speed | O(n) | O(n) | O(1) | O(1) |
| Use for | General | Fixed data | Unique items | Key-value pairs |

---

## Quick Reference

```python
# CREATE
d = {}                          # empty
d = {"key": "value"}           # literal
d = dict(key="value")          # constructor
d = dict(zip(keys, values))    # from two lists
d = {k: v for k, v in items}  # comprehension

# ACCESS
d["key"]                       # direct — KeyError if missing
d.get("key")                   # safe — None if missing
d.get("key", default)          # safe with default
"key" in d                     # check key exists — O(1)
"val" in d.values()            # check value exists — O(n)

# ADD / UPDATE
d["key"] = value               # add or update
d.update(other_dict)           # merge in place
d.setdefault("key", default)   # set only if not exists

# REMOVE
d.pop("key")                   # remove + return — KeyError if missing
d.pop("key", default)          # remove + return — safe
d.popitem()                    # remove last inserted pair
del d["key"]                   # remove — KeyError if missing
d.clear()                      # empty the dict

# VIEW
d.keys()                       # all keys
d.values()                     # all values
d.items()                      # all key-value pairs as tuples

# ITERATE
for k in d:                    # keys
for k in d.keys():             # keys explicit
for v in d.values():           # values
for k, v in d.items():         # key-value pairs

# MERGE
{**d1, **d2}                   # new dict (3.5+)
d1 | d2                        # new dict (3.9+)
d1.update(d2)                  # in-place

# COLLECTIONS
from collections import defaultdict
from collections import Counter
Counter(list).most_common(n)   # top n frequent
defaultdict(list)              # auto-init list for missing keys
defaultdict(int)               # auto-init 0 for missing keys
```

---

## Interview Short Answers

**Q: What is a dictionary in Python?**
> A dictionary is a mutable, ordered (Python 3.7+) collection of key-value pairs. Keys must be unique and immutable — strings, numbers, and tuples can be keys but lists cannot. Values can be any type. Dictionary lookup, insertion, and deletion are all O(1) average time, making it the most important data structure for optimization problems.

**Q: Were dictionaries always ordered in Python?**
> No. Before Python 3.7, dictionaries were unordered — the insertion order was not guaranteed. From Python 3.7 onwards, dictionaries officially maintain insertion order. This is an implementation detail that became part of the language specification. Always mention this version dependency in interviews.

**Q: What is the difference between `dict[key]` and `dict.get(key)`?**
> `dict[key]` raises a `KeyError` if the key does not exist. `dict.get(key)` returns `None` by default if the key is missing, or a custom default if provided as the second argument: `dict.get(key, default)`. Always use `get()` when you are not sure if the key exists.

**Q: What is `defaultdict` and when do you use it?**
> `defaultdict` from the `collections` module is a dictionary subclass that automatically provides a default value for missing keys instead of raising `KeyError`. You specify a default factory like `int` (default 0) or `list` (default []). It is commonly used for frequency counting and building graph adjacency lists in DSA.

**Q: What is `Counter` and what can it do?**
> `Counter` from `collections` is a dictionary subclass that counts the frequency of elements in an iterable. It supports `most_common(n)` to get the top N frequent elements, and arithmetic operations like adding and subtracting counts. It is used for anagram checks, frequency analysis, and top-K element problems.

**Q: What is the time complexity of dictionary operations?**
> All core dictionary operations — access, insert, delete, and key search — are O(1) on average. This is because dictionaries are implemented as hash tables. Worst case is O(n) due to hash collisions, but this is extremely rare in practice. Iteration over a dictionary is O(n).

**Q: How do you merge two dictionaries?**
> There are three main ways. `{**d1, **d2}` creates a new merged dictionary and works from Python 3.5+. `d1 | d2` creates a new merged dictionary and requires Python 3.9+. `d1.update(d2)` merges d2 into d1 in place. In all cases, if both dicts have the same key, the second dict's value wins.

**Q: What is the difference between `pop()` and `popitem()`?**
> `pop(key)` removes and returns the value for a specified key, raising `KeyError` if the key does not exist. `popitem()` removes and returns the last inserted key-value pair as a tuple — you do not specify which pair to remove. `popitem()` is useful for iterating and removing items from a dict simultaneously.
