# Lists in Python

## 1. What is a List?

A list is a collection of items that are:
- **Ordered** — elements maintain their insertion order
- **Mutable** — you can change, add, or remove elements after creation
- **Allow duplicates** — same value can appear multiple times
- **Heterogeneous** — can hold different data types in the same list

```python
fruits  = ["apple", "banana", "cherry"]   # strings
numbers = [1, 2, 3, 4, 5]                 # integers
mixed   = ["apple", 3, True, 3.14]        # mixed types
empty   = []                               # empty list
nested  = [[1, 2], [3, 4]]                # nested list
```

**Where to use:**
- Storing ordered collections (shopping cart, student marks)
- When you need to add/remove items dynamically
- When duplicates are allowed
- As a stack or queue in DSA problems

---

## 2. List Indexing

Every element has a **positive index** (left to right) and a **negative index** (right to left).

```
List:      a p p l e  b a n a n a  c h e r r y
Positive:  0          1             2
Negative: -3         -2            -1
```

```python
fruits = ["apple", "banana", "cherry"]

# Positive indexing
print(fruits[0])    # Output: apple
print(fruits[1])    # Output: banana
print(fruits[2])    # Output: cherry

# Negative indexing (from the end)
print(fruits[-1])   # Output: cherry  (last element)
print(fruits[-2])   # Output: banana
print(fruits[-3])   # Output: apple   (same as fruits[0])
```

> ⚠️ Accessing an index that doesn't exist raises `IndexError`:
> ```python
> print(fruits[5])   # IndexError: list index out of range
> ```

---

## 3. Modifying Lists

Lists are mutable — the object itself can be changed in place.

### Changing a Specific Element
```python
fruits = ["apple", "banana", "cherry"]
fruits[1] = "orange"
print(fruits)   # Output: ['apple', 'orange', 'cherry']
```

### Adding Elements

**`append(x)`** — adds one element to the **end**. O(1) time.
```python
fruits.append("grape")
print(fruits)   # Output: ['apple', 'orange', 'cherry', 'grape']

# Where to use: building a list dynamically in a loop
result = []
for i in range(5):
    result.append(i * 2)
print(result)   # Output: [0, 2, 4, 6, 8]
```

**`insert(index, value)`** — inserts at a specific position. O(n) time — shifts all elements after it.
```python
fruits.insert(1, "kiwi")
print(fruits)   # Output: ['apple', 'kiwi', 'orange', 'cherry']
```

**`extend(iterable)`** — adds **all elements** from another iterable. O(k) where k = length of iterable.
```python
fruits.extend(["mango", "papaya"])
print(fruits)

# append vs extend — KEY DIFFERENCE
a = [1, 2]
a.append([3, 4])   # adds the list AS ONE element → [1, 2, [3, 4]]
print(a)

a = [1, 2]
a.extend([3, 4])   # unpacks and adds each element → [1, 2, 3, 4]
print(a)
```

### Removing Elements

**`remove(value)`** — removes the **first occurrence** by value. O(n) time.
```python
fruits = ["apple", "kiwi", "apple", "cherry"]
fruits.remove("apple")   # removes first "apple" only
print(fruits)            # Output: ['kiwi', 'apple', 'cherry']

# ⚠️ Raises ValueError if element not found
try:
    fruits.remove("mango")
except ValueError:
    print("Not found!")
```

**`pop(index)`** — removes and **returns** the element. O(1) for last, O(n) for others.
```python
fruits = ["apple", "kiwi", "cherry"]

last = fruits.pop()      # removes last item — O(1)
print(last)              # Output: cherry

first = fruits.pop(0)    # removes first item — O(n) — shifts everything
print(first)             # Output: apple

# pop() returning the value is useful
numbers = [10, 20, 30, 40]
removed = numbers.pop(2)
print(removed)    # Output: 30
print(numbers)    # Output: [10, 20, 40]
```

**`del` keyword** — deletes by index or slice. Does **not return** the value.
```python
numbers = [10, 20, 30, 40, 50]
del numbers[2]        # removes 30
print(numbers)        # Output: [10, 20, 40, 50]

del numbers[1:3]      # removes a slice
print(numbers)        # Output: [10, 50]

del numbers           # deletes the entire variable
```

**`clear()`** — removes all elements, list becomes empty.
```python
fruits = ["apple", "banana"]
fruits.clear()
print(fruits)   # Output: []
```

---

## 4. Slicing Lists

Extract a portion of a list — creates a **new list** (does not modify original).

```
Syntax: list[start : stop : step]
```

- `start` — inclusive, default 0
- `stop`  — exclusive, default end of list
- `step`  — default 1, can be negative

```python
numbers = [0, 1, 2, 3, 4, 5, 6]

print(numbers[1:4])    # Output: [1, 2, 3]      (index 1 to 3)
print(numbers[:4])     # Output: [0, 1, 2, 3]   (from start to 3)
print(numbers[2:])     # Output: [2, 3, 4, 5, 6](from index 2 to end)
print(numbers[::2])    # Output: [0, 2, 4, 6]   (every 2nd element)
print(numbers[::-1])   # Output: [6, 5, 4, 3, 2, 1, 0]  (reversed)
print(numbers[4:1:-1]) # Output: [4, 3, 2]      (reverse slice)

# Full copy using slice
copy = numbers[:]
print(copy is numbers)   # Output: False — new object
```

**💡 DSA Tip:** `list[::-1]` to reverse is O(n) and creates a new list. `list.reverse()` reverses in place without creating a new list.

---

## 5. List Operators

### Concatenation (`+`) — creates a new list
```python
a = [1, 2, 3]
b = [4, 5, 6]
print(a + b)    # Output: [1, 2, 3, 4, 5, 6]
# Note: + creates a new list. extend() modifies in place.
```

### Repetition (`*`)
```python
print([0] * 5)      # Output: [0, 0, 0, 0, 0]
print([1, 2] * 3)   # Output: [1, 2, 1, 2, 1, 2]

# Common DSA use: initialize a fixed-size list
dp = [0] * 10       # create array of 10 zeros for dynamic programming
```

### Membership (`in` / `not in`) — O(n) time
```python
fruits = ["apple", "banana", "cherry"]
print("apple" in fruits)       # Output: True
print("mango" not in fruits)   # Output: True
```

> ⚠️ `in` on a list is **O(n)** — it checks every element. For O(1) lookup use a `set` or `dict`.

---

## 6. List Functions and Methods

### 6.1 Built-in Functions

**`len(list)`** — O(1) time — Python stores length internally
```python
print(len([1, 2, 3]))   # Output: 3
```

**`sum(list)`** — O(n) — adds all elements
```python
print(sum([1, 2, 3, 4]))   # Output: 10
```

**`min(list)` / `max(list)`** — O(n)
```python
numbers = [3, 1, 9, 5]
print(min(numbers))   # Output: 1
print(max(numbers))   # Output: 9
```

**`sorted(list)`** — returns a **new sorted list**, original unchanged. O(n log n).
```python
numbers = [5, 2, 9, 1]
print(sorted(numbers))                # Output: [1, 2, 5, 9]
print(sorted(numbers, reverse=True))  # Output: [9, 5, 2, 1]
print(numbers)                        # Output: [5, 2, 9, 1]  — unchanged

# key= parameter
words = ["banana", "kiwi", "apple"]
print(sorted(words, key=len))         # Output: ['kiwi', 'apple', 'banana']

# Sort by second element of each tuple
pairs = [(1, 3), (2, 1), (3, 2)]
print(sorted(pairs, key=lambda x: x[1]))  # Output: [(2,1), (3,2), (1,3)]
```

**`enumerate(list)`** — gives index + value pairs
```python
fruits = ["apple", "banana", "cherry"]
for index, fruit in enumerate(fruits):
    print(index, fruit)
# 0 apple
# 1 banana
# 2 cherry

for index, fruit in enumerate(fruits, start=1):  # start from 1
    print(index, fruit)
```

**`zip(list1, list2)`** — iterate two lists together
```python
names  = ["Aj", "Rahul", "Priya"]
scores = [95, 87, 92]

for name, score in zip(names, scores):
    print(f"{name}: {score}")
# Aj: 95
# Rahul: 87
# Priya: 92

# Create dict from two lists
student_dict = dict(zip(names, scores))
print(student_dict)   # {'Aj': 95, 'Rahul': 87, 'Priya': 92}
```

### 6.2 List Methods

**`sort()`** — sorts **in place**, modifies original. O(n log n).
```python
numbers = [5, 2, 9, 1]
numbers.sort()
print(numbers)               # Output: [1, 2, 5, 9]

numbers.sort(reverse=True)
print(numbers)               # Output: [9, 5, 2, 1]
```

> **`sort()` vs `sorted()`:**
> | | `sort()` | `sorted()` |
> |---|---|---|
> | Modifies original? | ✅ Yes (in place) | ❌ No (new list) |
> | Returns | `None` | New sorted list |
> | Works on | Lists only | Any iterable |

**`reverse()`** — reverses in place. O(n).
```python
fruits = ["apple", "banana", "cherry"]
fruits.reverse()
print(fruits)   # Output: ['cherry', 'banana', 'apple']
```

**`index(element)`** — returns index of first occurrence. Raises `ValueError` if not found.
```python
fruits = ["apple", "banana", "apple"]
print(fruits.index("apple"))    # Output: 0  (first occurrence only)

try:
    print(fruits.index("mango"))
except ValueError:
    print("Not found!")
```

**`count(element)`** — counts occurrences. O(n).
```python
numbers = [1, 2, 3, 1, 1]
print(numbers.count(1))   # Output: 3
```

**`copy()`** — shallow copy. O(n).
```python
original  = [1, 2, 3]
copy_list = original.copy()
copy_list.append(4)
print(original)    # Output: [1, 2, 3]   — unchanged
print(copy_list)   # Output: [1, 2, 3, 4]
```

---

## 7. Shallow vs Deep Copy

```python
import copy

original = [[1, 2], [3, 4]]

# Shallow copy — outer list is new, but inner lists still shared
shallow = original.copy()
shallow[0].append(99)
print(original)   # Output: [[1, 2, 99], [3, 4]]  ← affected!

# Deep copy — completely independent at all levels
original = [[1, 2], [3, 4]]
deep = copy.deepcopy(original)
deep[0].append(99)
print(original)   # Output: [[1, 2], [3, 4]]  ← unaffected
```

```
Shallow Copy:
original ──→ [ [1,2] , [3,4] ]
                ↑         ↑
shallow  ──→ [  ↑   ,    ↑   ]   ← inner lists still shared!

Deep Copy:
original ──→ [ [1,2] , [3,4] ]
deep     ──→ [ [1,2] , [3,4] ]   ← completely new objects at all levels
```

---

## 8. List Comprehension

A compact, readable way to create lists. **Faster than a regular for loop.**

```python
# Syntax
new_list = [expression for item in iterable if condition]
```

```python
# Squares
squares = [x**2 for x in range(6)]
print(squares)   # Output: [0, 1, 4, 9, 16, 25]

# Filter even numbers
evens = [x for x in range(10) if x % 2 == 0]
print(evens)     # Output: [0, 2, 4, 6, 8]

# Uppercase
fruits = ["apple", "banana", "cherry"]
upper  = [f.upper() for f in fruits]
print(upper)     # Output: ['APPLE', 'BANANA', 'CHERRY']

# Nested comprehension — flatten a matrix
matrix  = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
flat    = [num for row in matrix for num in row]
print(flat)      # Output: [1, 2, 3, 4, 5, 6, 7, 8, 9]

# With condition — filter and transform together
result = [x**2 for x in range(10) if x % 2 == 0]
print(result)    # Output: [0, 4, 16, 36, 64]
```

**💡 DSA Tip:** List comprehension is O(n) same as a loop but typically 30-50% faster due to internal optimization. Use it to impress interviewers with clean code.

---

## 9. Unpacking a List

```python
a, b, c = [1, 2, 3]
print(a, b, c)    # Output: 1 2 3

# *rest — collect remaining elements
first, *rest = [10, 20, 30, 40]
print(first)      # Output: 10
print(rest)       # Output: [20, 30, 40]

# first and last
first, *middle, last = [1, 2, 3, 4, 5]
print(first)      # Output: 1
print(middle)     # Output: [2, 3, 4]
print(last)       # Output: 5

# Swap using unpacking
a, b = 5, 10
a, b = b, a
print(a, b)       # Output: 10 5
```

---

## 10. Nested Lists — 2D Matrix

```python
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

print(matrix[0])       # Output: [1, 2, 3]  — first row
print(matrix[1][1])    # Output: 5           — row 2, col 2
print(matrix[2][0])    # Output: 7           — row 3, col 1

# Traverse entire matrix
for row in matrix:
    for element in row:
        print(element, end=" ")
    print()

# Transpose a matrix
transposed = [[matrix[j][i] for j in range(len(matrix))]
               for i in range(len(matrix[0]))]
print(transposed)   # Output: [[1,4,7],[2,5,8],[3,6,9]]
```

---

## 11. List as Stack and Queue

### Stack — LIFO (Last In First Out)
Use `append()` to push, `pop()` to pop — both O(1).

```python
stack = []

stack.append(10)    # push
stack.append(20)
stack.append(30)
print(stack)        # Output: [10, 20, 30]

print(stack.pop())  # Output: 30  — last in, first out
print(stack.pop())  # Output: 20
print(stack)        # Output: [10]
```

### Queue — FIFO (First In First Out)
Use `append()` to enqueue, `pop(0)` to dequeue — but `pop(0)` is **O(n)**.

```python
from collections import deque   # use deque for O(1) queue operations

queue = deque()
queue.append(10)     # enqueue
queue.append(20)
queue.append(30)

print(queue.popleft())   # Output: 10  — first in, first out
print(queue.popleft())   # Output: 20
```

> **Interview answer:** Use a plain list as a stack (append/pop = O(1)). For a queue, use `collections.deque` — `popleft()` is O(1) vs `pop(0)` on a list which is O(n).

---

## 12. Time Complexity — Must Know for Interviews

| Operation | Method | Time Complexity |
|---|---|---|
| Access by index | `list[i]` | O(1) |
| Get length | `len(list)` | O(1) |
| Add to end | `append(x)` | O(1) amortized |
| Add to middle/start | `insert(i, x)` | O(n) |
| Remove from end | `pop()` | O(1) |
| Remove from middle/start | `pop(i)` / `remove(x)` | O(n) |
| Search | `x in list` | O(n) |
| Sort | `sort()` / `sorted()` | O(n log n) |
| Reverse | `reverse()` | O(n) |
| Slice | `list[a:b]` | O(k) — k = slice size |
| Copy | `copy()` | O(n) |

> **Most asked in interviews:** "What is the time complexity of `insert(0, x)`?" → O(n) because all elements shift right.

---

## 13. DSA Patterns Using Lists

### Two Pointer Technique
```python
# Check if array is palindrome using two pointers
arr = [1, 2, 3, 2, 1]
left, right = 0, len(arr) - 1

is_palindrome = True
while left < right:
    if arr[left] != arr[right]:
        is_palindrome = False
        break
    left  += 1
    right -= 1

print(is_palindrome)   # Output: True
```

### Sliding Window
```python
# Find max sum of k consecutive elements
arr = [2, 1, 5, 1, 3, 2]
k   = 3

window_sum = sum(arr[:k])
max_sum    = window_sum

for i in range(k, len(arr)):
    window_sum += arr[i] - arr[i - k]   # slide the window
    max_sum = max(max_sum, window_sum)

print(max_sum)   # Output: 9  (5+1+3)
```

### Frequency Counter
```python
# Count frequency of each element
arr  = [1, 2, 3, 1, 2, 1]
freq = {}

for num in arr:
    freq[num] = freq.get(num, 0) + 1

print(freq)   # Output: {1: 3, 2: 2, 3: 1}
```

---

## Quick Reference

```python
# CREATE
lst = []                    # empty
lst = [1, 2, 3]             # with values
lst = [0] * 5               # [0,0,0,0,0]
lst = list(range(5))        # [0,1,2,3,4]
lst = [x**2 for x in range(5)]  # comprehension

# ACCESS
lst[0]          # first
lst[-1]         # last
lst[1:4]        # slice
lst[::-1]       # reversed

# ADD
lst.append(x)       # O(1) — end
lst.insert(i, x)    # O(n) — middle
lst.extend(other)   # O(k)

# REMOVE
lst.pop()           # O(1) — last
lst.pop(i)          # O(n) — by index
lst.remove(x)       # O(n) — by value
del lst[i]          # O(n) — no return
lst.clear()         # empty the list

# INFO
len(lst)            # O(1)
lst.count(x)        # O(n)
lst.index(x)        # O(n)
x in lst            # O(n)

# SORT
lst.sort()              # in place
sorted(lst)             # new list
lst.reverse()           # in place
lst[::-1]               # new reversed list

# COPY
lst.copy()              # shallow
copy.deepcopy(lst)      # deep — for nested lists

# ITERATE
for item in lst:
for i, item in enumerate(lst):
for a, b in zip(lst1, lst2):
```

---

## Interview Short Answers

**Q: What is a list in Python?**
> A list is an ordered, mutable, and indexed collection that allows duplicate elements. It can store items of different data types. Lists maintain insertion order and support dynamic resizing.

**Q: What is the difference between `append()` and `extend()`?**
> `append()` adds its argument as a single element to the end of the list — so `append([3,4])` adds the entire list as one element. `extend()` iterates over its argument and adds each element individually — so `extend([3,4])` adds two separate elements. `append()` is O(1), `extend()` is O(k) where k is the length of the iterable.

**Q: What is the difference between `pop()` and `remove()`?**
> `pop(i)` removes and returns the element at a given index — default is the last element. `remove(x)` searches for the first occurrence of a value and removes it without returning it. `pop()` on the last element is O(1), `remove()` is O(n) because it searches first.

**Q: What is the difference between `sort()` and `sorted()`?**
> `sort()` sorts the list in place and returns `None` — the original list is modified. `sorted()` returns a new sorted list and leaves the original unchanged. `sort()` works only on lists, `sorted()` works on any iterable.

**Q: What is the time complexity of inserting at the beginning of a list?**
> O(n) — because all existing elements must shift one position to the right to make room at index 0. For frequent insertions at the start, use `collections.deque` which supports O(1) insertion at both ends.

**Q: What is the difference between shallow copy and deep copy?**
> A shallow copy creates a new list but the nested objects inside still reference the same memory locations as the original. So modifying a nested list in the copy affects the original. A deep copy creates completely new objects at all levels — fully independent from the original. Use `copy.deepcopy()` for nested lists.

**Q: Why is `pop(0)` slow on a list?**
> `pop(0)` removes the first element and then shifts every remaining element one position to the left — O(n). Use `collections.deque` with `popleft()` for O(1) removal from the front, which is what makes it ideal for queue operations.

**Q: How is a list used as a stack?**
> Use `append()` to push an element onto the stack and `pop()` to remove from the top. Both are O(1) operations. This gives Last In First Out (LIFO) behavior which is exactly what a stack needs.
