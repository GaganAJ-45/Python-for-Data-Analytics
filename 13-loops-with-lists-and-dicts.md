# Loops with Lists and Dictionaries

## 1. What This File Covers

This file bridges loops with the two most important data structures — **lists** and **dictionaries**. Almost every real-world Python program and DSA problem combines these three concepts. Mastering this combination is essential for interviews.

---

## 2. Looping Over Lists

### Basic Traversal
```python
students = ["AJ", "Rahul", "Priya", "Divya"]

# By value — when you only need the element
for student in students:
    print(student)

# By index — when you need position
for i in range(len(students)):
    print(f"{i}: {students[i]}")

# By index + value — best of both
for i, student in enumerate(students):
    print(f"{i}: {student}")
```

### Modifying List While Iterating — Common Mistake
```python
# ❌ WRONG — never modify a list while iterating over it
numbers = [1, 2, 3, 4, 5]
for num in numbers:
    if num % 2 == 0:
        numbers.remove(num)   # skips elements!
print(numbers)   # Output: [1, 3, 5] — looks right but...

# Test with [2, 4, 6]
numbers = [2, 4, 6]
for num in numbers:
    if num % 2 == 0:
        numbers.remove(num)
print(numbers)   # Output: [4] ← WRONG! 4 was skipped

# ✅ CORRECT — iterate over a copy
numbers = [2, 4, 6]
for num in numbers[:]:    # numbers[:] is a copy
    if num % 2 == 0:
        numbers.remove(num)
print(numbers)   # Output: []

# ✅ BETTER — use list comprehension
numbers = [2, 4, 6, 1, 3, 5]
numbers = [n for n in numbers if n % 2 != 0]
print(numbers)   # Output: [1, 3, 5]
```

> **Interview tip:** Modifying a list while iterating over it causes skipped elements or missed removals — a very common bug. Always iterate over a copy or use list comprehension to filter.

---

## 3. Building Lists with Loops

### Accumulate results
```python
# Collect squares of even numbers
result = []
for i in range(1, 11):
    if i % 2 == 0:
        result.append(i ** 2)
print(result)   # Output: [4, 16, 36, 64, 100]

# Same with comprehension
result = [i**2 for i in range(1, 11) if i % 2 == 0]
```

### Build list from user input
```python
numbers = []
n = int(input("How many numbers? "))
for _ in range(n):
    num = int(input("Enter number: "))
    numbers.append(num)
print("You entered:", numbers)
print("Sum:", sum(numbers))
print("Max:", max(numbers))
```

### Filter elements
```python
marks  = [45, 82, 67, 90, 38, 74]
passed = [m for m in marks if m >= 50]
failed = [m for m in marks if m < 50]
print("Passed:", passed)   # Output: [82, 67, 90, 74]
print("Failed:", failed)   # Output: [45, 38]
```

---

## 4. Searching in a List

### Linear Search
```python
def search(lst, target):
    for i, val in enumerate(lst):
        if val == target:
            return i       # return index if found
    return -1              # -1 means not found

arr = [10, 25, 7, 60, 15]
print(search(arr, 60))    # Output: 3
print(search(arr, 99))    # Output: -1
```

### Find All Occurrences
```python
def find_all(lst, target):
    return [i for i, val in enumerate(lst) if val == target]

arr = [1, 2, 3, 1, 2, 1]
print(find_all(arr, 1))   # Output: [0, 3, 5]
```

---

## 5. Sorting and Ranking with Loops

```python
marks   = [("AJ", 85), ("Rahul", 92), ("Priya", 78)]

# Sort by marks — ascending
marks.sort(key=lambda x: x[1])
print(marks)

# Sort by marks — descending
marks.sort(key=lambda x: x[1], reverse=True)
print(marks)

# Print rank
for rank, (name, score) in enumerate(marks, start=1):
    print(f"Rank {rank}: {name} — {score}")
# Rank 1: Rahul — 92
# Rank 2: AJ — 85
# Rank 3: Priya — 78
```

---

## 6. Two Lists Together — `zip()`

```python
names  = ["AJ", "Rahul", "Priya"]
scores = [85, 92, 78]

# Print together
for name, score in zip(names, scores):
    print(f"{name}: {score}")

# Find who passed
passing_score = 80
for name, score in zip(names, scores):
    status = "Pass" if score >= passing_score else "Fail"
    print(f"{name}: {status}")

# Create list of dicts
students = [{"name": n, "score": s} for n, s in zip(names, scores)]
print(students)
# [{'name': 'AJ', 'score': 85}, {'name': 'Rahul', 'score': 92}, ...]
```

---

## 7. Looping Over Dictionaries

### 4 Ways to Iterate
```python
karnataka = {
    "Bengaluru" : "Bisi Bele Bath",
    "Mysuru"    : "Mysore Pak",
    "Mangaluru" : "Neer Dosa",
    "Shivamogga": "Kadubu"
}

# Keys only (default)
for city in karnataka:
    print(city)

# Keys explicit
for city in karnataka.keys():
    print(city)

# Values only
for dish in karnataka.values():
    print(dish)

# Key-value pairs — most useful
for city, dish in karnataka.items():
    print(f"{city} is famous for {dish}")
```

### Filter Dictionary
```python
scores = {"AJ": 85, "Rahul": 55, "Priya": 92, "Divya": 48}

# Students who passed
passed = {name: score for name, score in scores.items() if score >= 60}
print(passed)   # Output: {'AJ': 85, 'Priya': 92}

# Students who failed
failed = {name: score for name, score in scores.items() if score < 60}
print(failed)   # Output: {'Rahul': 55, 'Divya': 48}
```

### Sort Dictionary by Value
```python
scores = {"AJ": 85, "Rahul": 55, "Priya": 92, "Divya": 48}

# Sort by value — ascending
sorted_scores = sorted(scores.items(), key=lambda x: x[1])
print(sorted_scores)
# [('Divya', 48), ('Rahul', 55), ('AJ', 85), ('Priya', 92)]

# Sort by value — descending (leaderboard)
sorted_scores = sorted(scores.items(), key=lambda x: x[1], reverse=True)
for rank, (name, score) in enumerate(sorted_scores, start=1):
    print(f"Rank {rank}: {name} — {score}")
```

---

## 8. Building Dictionaries with Loops

### Frequency Counter — most common DSA pattern
```python
# Character frequency
word  = "banana"
freq  = {}
for char in word:
    freq[char] = freq.get(char, 0) + 1
print(freq)   # Output: {'b': 1, 'a': 3, 'n': 2}

# Word frequency
text  = "the cat sat on the mat the cat"
freq  = {}
for word in text.split():
    freq[word] = freq.get(word, 0) + 1
print(freq)
# {'the': 3, 'cat': 2, 'sat': 1, 'on': 1, 'mat': 1}
```

### Group items by property
```python
students = [
    {"name": "AJ",    "grade": "A"},
    {"name": "Rahul", "grade": "B"},
    {"name": "Priya", "grade": "A"},
    {"name": "Divya", "grade": "B"},
    {"name": "Kiran", "grade": "A"},
]

# Group by grade
groups = {}
for student in students:
    grade = student["grade"]
    if grade not in groups:
        groups[grade] = []
    groups[grade].append(student["name"])

print(groups)
# {'A': ['AJ', 'Priya', 'Kiran'], 'B': ['Rahul', 'Divya']}
```

### Index → value mapping
```python
fruits = ["apple", "banana", "cherry"]
index_map = {fruit: i for i, fruit in enumerate(fruits)}
print(index_map)   # {'apple': 0, 'banana': 1, 'cherry': 2}
```

---

## 9. Nested Lists — 2D Matrix Traversal

```python
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

# Traverse all elements
for row in matrix:
    for element in row:
        print(element, end=" ")
    print()
# 1 2 3
# 4 5 6
# 7 8 9

# Find sum of each row
for i, row in enumerate(matrix):
    print(f"Row {i} sum: {sum(row)}")

# Find max in entire matrix
max_val = matrix[0][0]
for row in matrix:
    for val in row:
        if val > max_val:
            max_val = val
print("Max:", max_val)   # Output: 9
```

---

## 10. List of Dictionaries — Most Common Real-World Pattern

```python
students = [
    {"name": "AJ",    "age": 22, "marks": 85},
    {"name": "Rahul", "age": 21, "marks": 92},
    {"name": "Priya", "age": 23, "marks": 78},
]

# Print all students
for student in students:
    print(f"{student['name']} — Marks: {student['marks']}")

# Find topper
topper = max(students, key=lambda s: s["marks"])
print(f"Topper: {topper['name']} with {topper['marks']}")

# Filter students who scored above 80
top_students = [s for s in students if s["marks"] > 80]
print(top_students)

# Calculate average marks
avg = sum(s["marks"] for s in students) / len(students)
print(f"Average: {avg:.2f}")

# Sort by marks descending
students.sort(key=lambda s: s["marks"], reverse=True)
for rank, s in enumerate(students, 1):
    print(f"Rank {rank}: {s['name']} — {s['marks']}")
```

---

## 11. DSA Patterns — Lists + Dicts + Loops

### Two Sum — O(n) with dict
```python
def two_sum(arr, target):
    seen = {}   # value → index
    for i, num in enumerate(arr):
        complement = target - num
        if complement in seen:
            return [seen[complement], i]
        seen[num] = i
    return []

print(two_sum([2, 7, 4, 3], 10))   # Output: [1, 2]
```

### Find Duplicates
```python
def find_duplicates(arr):
    freq = {}
    for num in arr:
        freq[num] = freq.get(num, 0) + 1
    return [num for num, count in freq.items() if count > 1]

print(find_duplicates([1, 2, 3, 2, 4, 3, 5]))   # Output: [2, 3]
```

### Anagram Check
```python
def is_anagram(s1, s2):
    if len(s1) != len(s2):
        return False
    freq = {}
    for char in s1:
        freq[char] = freq.get(char, 0) + 1
    for char in s2:
        if char not in freq or freq[char] == 0:
            return False
        freq[char] -= 1
    return True

print(is_anagram("listen", "silent"))   # Output: True
print(is_anagram("hello", "world"))     # Output: False
```

### Group Anagrams
```python
def group_anagrams(words):
    groups = {}
    for word in words:
        key = "".join(sorted(word))   # sorted letters as key
        if key not in groups:
            groups[key] = []
        groups[key].append(word)
    return list(groups.values())

words = ["eat", "tea", "tan", "ate", "nat", "bat"]
print(group_anagrams(words))
# [['eat', 'tea', 'ate'], ['tan', 'nat'], ['bat']]
```

### Sliding Window — Max Sum of K Elements
```python
def max_sum_subarray(arr, k):
    window_sum = sum(arr[:k])
    max_sum    = window_sum

    for i in range(k, len(arr)):
        window_sum += arr[i] - arr[i - k]
        max_sum = max(max_sum, window_sum)

    return max_sum

arr = [2, 1, 5, 1, 3, 2]
print(max_sum_subarray(arr, 3))   # Output: 9  (5+1+3)
```

---

## Quick Reference

```python
# LIST + LOOP
for item in lst:                        # by value
for i in range(len(lst)):               # by index
for i, item in enumerate(lst):          # both
for a, b in zip(lst1, lst2):            # two lists

# BUILD LIST WITH LOOP
result = []
for x in lst:
    result.append(transform(x))
# Better:
result = [transform(x) for x in lst]
result = [x for x in lst if condition]

# DICT + LOOP
for k in d:                             # keys
for k in d.keys():                      # keys
for v in d.values():                    # values
for k, v in d.items():                  # key-value

# BUILD DICT WITH LOOP
freq = {}
for item in lst:
    freq[item] = freq.get(item, 0) + 1

# BUILD DICT WITH COMPREHENSION
d = {k: v for k, v in zip(keys, values)}
d = {x: x**2 for x in range(5)}

# FILTER DICT
filtered = {k: v for k, v in d.items() if condition}

# SORT DICT BY VALUE
sorted_items = sorted(d.items(), key=lambda x: x[1])
sorted_items = sorted(d.items(), key=lambda x: x[1], reverse=True)

# LIST OF DICTS
max_item = max(lst, key=lambda x: x["field"])
filtered = [x for x in lst if x["field"] > value]
sorted_lst = sorted(lst, key=lambda x: x["field"])
avg = sum(x["field"] for x in lst) / len(lst)

# NEVER DO THIS
for item in lst:
    lst.remove(item)    # ❌ modifies while iterating
# Do this instead:
lst = [x for x in lst if not remove_condition(x)]
```

---

## Interview Short Answers

**Q: Why should you not modify a list while iterating over it?**
> When you remove an element from a list during iteration, the list shrinks and the iterator's internal index skips the next element. This causes elements to be silently missed. The fix is to iterate over a copy using `lst[:]` or filter using list comprehension, which creates a new list without modifying the original.

**Q: What is the most Pythonic way to iterate a list with index and value?**
> Use `enumerate()` — `for i, val in enumerate(lst)`. Avoid `range(len(lst))` — it is verbose and less readable. `enumerate()` takes an optional `start` parameter to begin counting from any number.

**Q: How do you sort a list of dictionaries by a field?**
> Use `sorted()` with a `key` function: `sorted(lst, key=lambda x: x["field"])`. For descending order add `reverse=True`. For in-place sorting use `lst.sort(key=lambda x: x["field"])`. Lambda extracts the field to sort by.

**Q: What is the frequency counter pattern?**
> The frequency counter pattern uses a dictionary to count occurrences of elements in a list or string. For each element, do `freq[item] = freq.get(item, 0) + 1`. This runs in O(n) and is used to solve anagram checks, duplicate finding, and top-K element problems — replacing nested loops that would be O(n²).

**Q: What is the sliding window technique?**
> Sliding window is a technique where you maintain a window of fixed or variable size and slide it across an array, updating the result incrementally instead of recomputing from scratch each time. For example, to find the maximum sum of k consecutive elements, compute the first window sum, then for each step add the new element and subtract the element that left the window. This converts O(n×k) to O(n).
