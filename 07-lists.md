# Lists in Python
> Complete Reference Notes

---

## 1. What is a List?

A list is a collection of items that are **ordered**, **mutable (changeable)**, and **allow duplicate elements**. Lists can hold items of different data types such as integers, strings, or even other lists.

**Syntax:**
```python
my_list = [element1, element2, element3, ...]
```

**Example:**
```python
fruits = ["apple", "banana", "cherry"]
numbers = [1, 2, 3, 4, 5]
mixed = ["apple", 3, True]
```

---

## 2. Accessing List Elements

Access individual elements using **indexing**. Python uses **zero-based indexing** (first item is at index 0).

**Syntax:**
```python
list_name[index]
```

**Example:**
```python
fruits = ["apple", "banana", "cherry"]
print(fruits[0])   # Output: apple
print(fruits[2])   # Output: cherry

# Negative indexing (from the end)
print(fruits[-1])  # Output: cherry
print(fruits[-2])  # Output: banana
```

---

## 3. Modifying Lists

Lists are mutable — you can change, add, or remove items.

### Changing a Specific Element
```python
fruits[1] = "orange"
print(fruits)  # Output: ['apple', 'orange', 'cherry']
```

### Adding Elements

- **`append()`** — Adds an element to the **end** of the list.
```python
fruits.append("grape")
print(fruits)  # Output: ['apple', 'orange', 'cherry', 'grape']
```

- **`insert(index, value)`** — Inserts an element at a **specific index**.
```python
fruits.insert(1, "kiwi")
print(fruits)  # Output: ['apple', 'kiwi', 'orange', 'cherry']
```

- **`extend(iterable)`** — Adds **all elements** from another list/iterable to the end.
```python
fruits.extend(["mango", "papaya"])
print(fruits)  # Output: ['apple', 'kiwi', 'orange', 'cherry', 'mango', 'papaya']

# Note: append() adds the whole object; extend() unpacks it
a = [1, 2]
a.append([3, 4])  # Result: [1, 2, [3, 4]]
a.extend([3, 4])  # Result: [1, 2, 3, 4]
```

### Removing Elements

- **`remove(value)`** — Removes the first occurrence of a value (uses value, not index).
```python
fruits.remove("orange")
print(fruits)  # Output: ['apple', 'kiwi', 'cherry']
```

- **`pop(index)`** — Removes and **returns** the element at the given index (last item if no index provided).
```python
fruits.pop()      # Removes last item
print(fruits)     # Output: ['apple', 'kiwi']

fruits.pop(0)     # Removes first item
print(fruits)     # Output: ['kiwi']

# pop() stores the removed value
numbers = [10, 20, 30, 40]
removed = numbers.pop(2)
print(removed)    # Output: 30
print(numbers)    # Output: [10, 20, 40]
```

- **`del` keyword** — Deletes an element or a slice by index. Unlike `pop()`, it does **not return** the removed value.
```python
numbers = [10, 20, 30, 40, 50]
del numbers[2]       # Removes 30
print(numbers)       # Output: [10, 20, 40, 50]

del numbers[1:3]     # Removes a slice
print(numbers)       # Output: [10, 50]
```

- **`clear()`** — Removes all elements from the list.
```python
fruits.clear()
print(fruits)  # Output: []
```

---

## 4. Slicing Lists

Extract a portion of a list using **slicing**.

**Syntax:**
```python
list_name[start:stop:step]
```

- `start` — Index to start the slice (inclusive).
- `stop` — Index to stop the slice (exclusive).
- `step` — How many elements to skip (default is 1).

**Examples:**
```python
numbers = [0, 1, 2, 3, 4, 5, 6]
print(numbers[1:4])   # Output: [1, 2, 3]
print(numbers[:4])    # Output: [0, 1, 2, 3]
print(numbers[2:])    # Output: [2, 3, 4, 5, 6]
print(numbers[::2])   # Output: [0, 2, 4, 6]
```

---

## 5. List Operators

### Concatenation (`+`)
Joins two lists together into a new list.
```python
a = [1, 2, 3]
b = [4, 5, 6]
print(a + b)   # Output: [1, 2, 3, 4, 5, 6]
```

### Repetition (`*`)
Repeats a list a given number of times.
```python
print([0] * 4)       # Output: [0, 0, 0, 0]
print(["ha"] * 3)    # Output: ['ha', 'ha', 'ha']
```

### Membership (`in` / `not in`)
Checks whether an element exists in a list. Returns `True` or `False`.
```python
fruits = ["apple", "banana", "cherry"]
print("apple" in fruits)       # Output: True
print("mango" not in fruits)   # Output: True
```

---

## 6. List Functions and Methods

### 6.1 Built-in Functions

- **`len(list)`** — Returns the number of elements.
```python
print(len(fruits))  # Output: 3
```

- **`sum(list)`** — Returns the sum of all elements (numerical lists).
```python
numbers = [1, 2, 3, 4]
print(sum(numbers))  # Output: 10
```

- **`min(list)` / `max(list)`** — Returns the smallest or largest element.
```python
numbers = [3, 1, 9, 5]
print(min(numbers))  # Output: 1
print(max(numbers))  # Output: 9
```

- **`sorted(list)`** — Returns a **new sorted list**. Original list is unchanged. Supports optional `reverse=True` and `key=` parameters.
```python
numbers = [5, 2, 9, 1]
print(sorted(numbers))                # Output: [1, 2, 5, 9]
print(sorted(numbers, reverse=True))  # Output: [9, 5, 2, 1]

# key= example: sort strings by length
words = ["banana", "kiwi", "apple"]
print(sorted(words, key=len))         # Output: ['kiwi', 'apple', 'banana']

print(numbers)  # Original unchanged: [5, 2, 9, 1]
```

### 6.2 List Methods

- **`sort()`** — Sorts the list **in place** (modifies original). Also supports `reverse=True` and `key=`.
```python
numbers = [5, 2, 9, 1]
numbers.sort()
print(numbers)               # Output: [1, 2, 5, 9]

numbers.sort(reverse=True)
print(numbers)               # Output: [9, 5, 2, 1]
```

- **`reverse()`** — Reverses the list in place.
```python
fruits = ["apple", "banana", "cherry"]
fruits.reverse()
print(fruits)  # Output: ['cherry', 'banana', 'apple']
```

- **`index(element)`** — Returns the index of the first occurrence of the element.
```python
print(fruits.index("apple"))  # Output: 0
```

- **`count(element)`** — Returns how many times an element appears.
```python
numbers = [1, 2, 3, 1, 1]
print(numbers.count(1))  # Output: 3
```

- **`copy()`** — Creates a shallow copy of the list.
```python
original = [1, 2, 3]
copy_list = original.copy()
copy_list.append(4)
print(original)    # Output: [1, 2, 3]   (unchanged)
print(copy_list)   # Output: [1, 2, 3, 4]
```

---

## 7. Shallow vs Deep Copy

`copy()` creates a **shallow copy** — the new list is independent, but nested lists inside still share the same reference. Use `deepcopy()` from the `copy` module to fully clone a nested structure.

```python
import copy

original = [[1, 2], [3, 4]]

# Shallow copy — inner lists still shared
shallow = original.copy()
shallow[0].append(99)
print(original)  # Output: [[1, 2, 99], [3, 4]]  <-- affected!

# Deep copy — fully independent
original = [[1, 2], [3, 4]]
deep = copy.deepcopy(original)
deep[0].append(99)
print(original)  # Output: [[1, 2], [3, 4]]  <-- unaffected
```

---

## 8. List Comprehension

A compact way to create lists from existing iterables. Much cleaner than writing a full `for` loop.

**Syntax:**
```python
new_list = [expression for item in iterable if condition]
```

**Examples:**
```python
# Squares of numbers 0–4
squares = [x**2 for x in range(5)]
print(squares)  # Output: [0, 1, 4, 9, 16]

# Only even numbers
evens = [x for x in range(10) if x % 2 == 0]
print(evens)    # Output: [0, 2, 4, 6, 8]

# Uppercase all fruits
fruits = ["apple", "banana", "cherry"]
upper = [f.upper() for f in fruits]
print(upper)    # Output: ['APPLE', 'BANANA', 'CHERRY']
```

---

## 9. Unpacking a List

Assign list elements directly to individual variables. The number of variables must match the list length (unless using `*` to collect extras).

```python
a, b, c = [1, 2, 3]
print(a, b, c)   # Output: 1 2 3

# Using * to collect remaining elements
first, *rest = [10, 20, 30, 40]
print(first)     # Output: 10
print(rest)      # Output: [20, 30, 40]
```

---

## 10. Iterating Over a List

### Using a `for` loop
```python
fruits = ["apple", "banana", "cherry"]
for fruit in fruits:
    print(fruit)
```

### Using `enumerate()`
`enumerate()` gives you both the **index** and the **value** while iterating.
```python
for index, fruit in enumerate(fruits):
    print(index, fruit)

# Output:
# 0 apple
# 1 banana
# 2 cherry

# Start index from 1
for index, fruit in enumerate(fruits, start=1):
    print(index, fruit)
```

---

## 11. Nested Lists

Lists can contain other lists — useful for matrix-like data structures.

```python
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

print(matrix[0])      # Output: [1, 2, 3]   (first row)
print(matrix[1][1])   # Output: 5            (row 2, column 2)
```

---

## Quick Reference — All Methods & Functions

```python
# FUNCTIONS
len(list)                           # Number of elements
sum(list)                           # Sum of elements
min(list)                           # Smallest element
max(list)                           # Largest element
sorted(list)                        # New sorted list (original unchanged)
sorted(list, reverse=True, key=fn)  # With options
enumerate(list)                     # Index + value pairs

# METHODS
list.append(x)                      # Add x to end
list.extend(iterable)               # Add all items from iterable
list.insert(i, x)                   # Insert x at index i
list.remove(x)                      # Remove first x (by value)
list.pop(i)                         # Remove & return item at index i
list.clear()                        # Remove all items
del list[i]                         # Delete item by index (no return)
list.sort()                         # Sort in place
list.sort(reverse=True, key=fn)     # With options
list.reverse()                      # Reverse in place
list.index(x)                       # Index of first x
list.count(x)                       # Count occurrences of x
list.copy()                         # Shallow copy

# OPERATORS
list1 + list2                       # Concatenation
list * n                            # Repetition
x in list                           # Membership check
x not in list                       # Membership check (negated)
```
