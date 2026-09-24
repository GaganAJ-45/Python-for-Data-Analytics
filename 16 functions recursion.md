# Functions in Python — Recursion


## 1. What is Recursion?

Recursion is when a **function calls itself** to solve a smaller version of the same problem. Each call reduces the problem until it reaches a **base case** — the simplest version that can be solved directly.

```
Big problem
    → smaller problem
        → smaller problem
            → BASE CASE (solved directly)
        ← result bubbles back up
    ← result bubbles back up
← final answer
```

**Every recursive function needs two things:**
1. **Base case** — condition to stop recursion (prevents infinite loop)
2. **Recursive case** — calls itself with a smaller/simpler input

```python
def countdown(n):
    if n == 0:          # BASE CASE — stop here
        print("Go!")
        return
    print(n)
    countdown(n - 1)    # RECURSIVE CASE — smaller problem

countdown(5)
# 5
# 4
# 3
# 2
# 1
# Go!
```

---

## 2. The Call Stack

Every function call is added to the **call stack**. With recursion, calls stack up until the base case, then unwind in reverse.

```python
def factorial(n):
    if n == 0:
        return 1
    return n * factorial(n - 1)

factorial(4)
```

```
Call stack builds up:
factorial(4) → 4 * factorial(3)
               factorial(3) → 3 * factorial(2)
                              factorial(2) → 2 * factorial(1)
                                             factorial(1) → 1 * factorial(0)
                                                            factorial(0) → 1  ← BASE CASE

Stack unwinds:
factorial(0) = 1
factorial(1) = 1 * 1 = 1
factorial(2) = 2 * 1 = 2
factorial(3) = 3 * 2 = 6
factorial(4) = 4 * 6 = 24
```

> ⚠️ **Recursion limit:** Python has a default recursion limit of 1000. Exceeding it raises `RecursionError`. Use `sys.setrecursionlimit(n)` to increase it — but this is a code smell. Deep recursion should be converted to iteration.

```python
import sys
print(sys.getrecursionlimit())    # Output: 1000
sys.setrecursionlimit(10000)      # increase limit
```

---

## 3. Classic Problems — Easy

### Factorial — n!
**Definition:** `n! = n × (n-1) × (n-2) × ... × 1`. `0! = 1`.

```python
def factorial(n):
    # Base case
    if n == 0 or n == 1:
        return 1
    # Recursive case
    return n * factorial(n - 1)

print(factorial(5))   # Output: 120  (5×4×3×2×1)
print(factorial(0))   # Output: 1
print(factorial(1))   # Output: 1
```

**Trace for factorial(4):**
```
factorial(4) = 4 × factorial(3)
                   = 3 × factorial(2)
                       = 2 × factorial(1)
                           = 1  ← base case
             = 4 × 3 × 2 × 1 = 24
```

---

### Sum of N Natural Numbers
```python
def sum_n(n):
    if n == 0:          # base case
        return 0
    return n + sum_n(n - 1)   # recursive case

print(sum_n(5))   # Output: 15  (5+4+3+2+1+0)
```

**Trace:**
```
sum_n(5) = 5 + sum_n(4)
               = 4 + sum_n(3)
                   = 3 + sum_n(2)
                       = 2 + sum_n(1)
                           = 1 + sum_n(0)
                               = 0  ← base case
         = 5+4+3+2+1+0 = 15
```

---

### Sum of Digits
```python
def sum_digits(n):
    if n == 0:
        return 0
    return (n % 10) + sum_digits(n // 10)

print(sum_digits(12345))   # Output: 15  (1+2+3+4+5)
print(sum_digits(999))     # Output: 27
```

---

### Reverse a String
```python
def reverse_string(s):
    if len(s) == 0:      # base case — empty string
        return s
    return s[-1] + reverse_string(s[:-1])

print(reverse_string("Python"))   # Output: nohtyP
print(reverse_string("hello"))    # Output: olleh
```

---

### Palindrome Check
```python
def is_palindrome(s):
    if len(s) <= 1:                          # base case
        return True
    if s[0] != s[-1]:                        # mismatch — not palindrome
        return False
    return is_palindrome(s[1:-1])            # check inner string

print(is_palindrome("racecar"))   # Output: True
print(is_palindrome("madam"))     # Output: True
print(is_palindrome("hello"))     # Output: False
```

---

### Print Array Elements
```python
def print_array(arr, index=0):
    if index == len(arr):   # base case — past end
        return
    print(arr[index])
    print_array(arr, index + 1)

print_array([10, 20, 30, 40])
# 10
# 20
# 30
# 40
```

---

## 4. Classic Problems — Medium

### Fibonacci Series
**Definition:** Each number is sum of previous two. 0, 1, 1, 2, 3, 5, 8, 13...

```python
# Basic — O(2ⁿ) — very slow for large n
def fibonacci(n):
    if n <= 1:              # base cases: fib(0)=0, fib(1)=1
        return n
    return fibonacci(n-1) + fibonacci(n-2)

print(fibonacci(7))   # Output: 13
```

**Why it's slow — repeated calculations:**
```
fibonacci(5)
├── fibonacci(4)
│   ├── fibonacci(3)
│   │   ├── fibonacci(2)  ← computed multiple times!
│   │   └── fibonacci(1)
│   └── fibonacci(2)      ← computed again!
└── fibonacci(3)           ← computed again!
```

**Optimized with memoization — O(n):**
```python
from functools import lru_cache

@lru_cache(maxsize=None)
def fibonacci(n):
    if n <= 1:
        return n
    return fibonacci(n-1) + fibonacci(n-2)

print(fibonacci(50))    # Output: 12586269025  (instant)
print(fibonacci(100))   # Output: 354224848179261915075 (instant)
```

**Manual memoization with dict:**
```python
memo = {}

def fibonacci(n):
    if n <= 1:
        return n
    if n in memo:
        return memo[n]        # return cached result
    memo[n] = fibonacci(n-1) + fibonacci(n-2)
    return memo[n]

print(fibonacci(50))   # instant
```

> **Interview tip:** Always mention the time complexity of naive recursive Fibonacci — O(2ⁿ). Then show how memoization brings it to O(n). This is one of the most asked optimization questions.

---

### Power — base^exponent
```python
# Simple — O(n)
def power(base, exp):
    if exp == 0:
        return 1
    return base * power(base, exp - 1)

# Fast exponentiation — O(log n) — divide and conquer
def fast_power(base, exp):
    if exp == 0:
        return 1
    if exp % 2 == 0:
        half = fast_power(base, exp // 2)
        return half * half          # base^n = (base^(n/2))²
    return base * fast_power(base, exp - 1)

print(fast_power(2, 10))   # Output: 1024
print(fast_power(3, 5))    # Output: 243
```

> **Interview tip:** Fast exponentiation (binary exponentiation) is O(log n) vs O(n) for naive approach. It is a classic divide-and-conquer recursion and is asked frequently.

---

### GCD — Euclidean Algorithm
```python
def gcd(a, b):
    if b == 0:              # base case
        return a
    return gcd(b, a % b)   # recursive case

print(gcd(48, 18))   # Output: 6
print(gcd(100, 75))  # Output: 25
```

**Trace for gcd(48, 18):**
```
gcd(48, 18) → gcd(18, 12) → gcd(12, 6) → gcd(6, 0) → 6
```

---

### Binary Search — Recursive
```python
def binary_search(arr, target, left, right):
    if left > right:          # base case — not found
        return -1

    mid = (left + right) // 2

    if arr[mid] == target:    # base case — found
        return mid
    elif arr[mid] < target:
        return binary_search(arr, target, mid + 1, right)
    else:
        return binary_search(arr, target, left, mid - 1)

arr = [1, 3, 5, 7, 9, 11, 13]
print(binary_search(arr, 7, 0, len(arr)-1))    # Output: 3
print(binary_search(arr, 6, 0, len(arr)-1))    # Output: -1
```

**Time complexity: O(log n)** — halves the search space each call.

---

### Flatten Nested List
```python
def flatten(lst):
    result = []
    for item in lst:
        if isinstance(item, list):
            result.extend(flatten(item))   # recurse into nested list
        else:
            result.append(item)
    return result

nested = [1, [2, 3], [4, [5, 6]], 7]
print(flatten(nested))   # Output: [1, 2, 3, 4, 5, 6, 7]

deeply_nested = [1, [2, [3, [4, [5]]]]]
print(flatten(deeply_nested))   # Output: [1, 2, 3, 4, 5]
```

---

## 5. Classic Problems — Hard

### Tower of Hanoi
**Problem:** Move n disks from source to destination using an auxiliary peg. Rules:
1. Only one disk at a time
2. A larger disk cannot go on top of a smaller one

```python
def hanoi(n, source, destination, auxiliary):
    if n == 1:    # base case — move single disk
        print(f"Move disk 1 from {source} to {destination}")
        return

    # Move n-1 disks from source to auxiliary (using destination)
    hanoi(n-1, source, auxiliary, destination)

    # Move the largest disk from source to destination
    print(f"Move disk {n} from {source} to {destination}")

    # Move n-1 disks from auxiliary to destination (using source)
    hanoi(n-1, auxiliary, destination, source)

hanoi(3, "A", "C", "B")
# Move disk 1 from A to C
# Move disk 2 from A to B
# Move disk 1 from C to B
# Move disk 3 from A to C
# Move disk 1 from B to A
# Move disk 2 from B to C
# Move disk 1 from A to C
```

**Number of moves = 2ⁿ - 1** — O(2ⁿ) time complexity.

---

### Merge Sort — O(n log n)
**Divide and conquer** — split array in half recursively, then merge sorted halves.

```python
def merge_sort(arr):
    if len(arr) <= 1:      # base case — single element is sorted
        return arr

    mid   = len(arr) // 2
    left  = merge_sort(arr[:mid])    # sort left half
    right = merge_sort(arr[mid:])    # sort right half

    return merge(left, right)

def merge(left, right):
    result = []
    i = j  = 0

    while i < len(left) and j < len(right):
        if left[i] <= right[j]:
            result.append(left[i])
            i += 1
        else:
            result.append(right[j])
            j += 1

    result.extend(left[i:])
    result.extend(right[j:])
    return result

arr = [38, 27, 43, 3, 9, 82, 10]
print(merge_sort(arr))   # Output: [3, 9, 10, 27, 38, 43, 82]
```

**Trace for [38, 27, 43, 3]:**
```
[38, 27, 43, 3]
├── [38, 27]     ├── [43, 3]
│   ├── [38]     │   ├── [43]
│   └── [27]     │   └── [3]
│   → [27, 38]   │   → [3, 43]
└───────────────────────────────
         merge([27,38], [3,43]) → [3, 27, 38, 43]
```

---

### Quick Sort — O(n log n) average
```python
def quick_sort(arr):
    if len(arr) <= 1:    # base case
        return arr

    pivot  = arr[len(arr) // 2]
    left   = [x for x in arr if x < pivot]
    middle = [x for x in arr if x == pivot]
    right  = [x for x in arr if x > pivot]

    return quick_sort(left) + middle + quick_sort(right)

arr = [3, 6, 8, 10, 1, 2, 1]
print(quick_sort(arr))   # Output: [1, 1, 2, 3, 6, 8, 10]
```

---

### Count Occurrences in Array
```python
def count_occurrences(arr, target, index=0):
    if index == len(arr):   # base case
        return 0
    current = 1 if arr[index] == target else 0
    return current + count_occurrences(arr, target, index + 1)

print(count_occurrences([1, 2, 3, 1, 2, 1], 1))   # Output: 3
```

---

### Generate All Subsets (Power Set)
```python
def subsets(arr, index=0):
    if index == len(arr):
        return [[]]    # base case — one subset: empty set

    rest = subsets(arr, index + 1)   # subsets without current element
    with_current = [[arr[index]] + s for s in rest]  # add current to each
    return rest + with_current

print(subsets([1, 2, 3]))
# [[], [3], [2], [2,3], [1], [1,3], [1,2], [1,2,3]]
```

---

## 6. Recursion vs Iteration

| | Recursion | Iteration |
|---|---|---|
| Code clarity | Cleaner for tree/graph problems | Cleaner for simple loops |
| Memory | O(n) stack space | O(1) space |
| Speed | Slower — function call overhead | Faster |
| Risk | Stack overflow for large n | No stack overflow |
| Use for | Trees, graphs, divide-and-conquer | Arrays, simple counting |
| Base case | Required | Loop condition |

```python
# Factorial — both approaches
# Recursive
def factorial_r(n):
    return 1 if n <= 1 else n * factorial_r(n-1)

# Iterative
def factorial_i(n):
    result = 1
    for i in range(2, n+1):
        result *= i
    return result

# For large n — iterative is safer
print(factorial_i(1000))   # works fine
print(factorial_r(1000))   # RecursionError!
```

> **Interview rule of thumb:**
> - Use recursion for **trees, graphs, divide-and-conquer** (natural recursive structure)
> - Use iteration for **arrays, counters, simple loops** (avoid stack overhead)
> - Any recursion can be converted to iteration using an explicit stack

---

## 7. Tail Recursion

A recursive call is **tail recursive** when the recursive call is the **last operation** — nothing happens after it returns.

```python
# NOT tail recursive — multiplication happens after recursive call
def factorial(n):
    if n == 0:
        return 1
    return n * factorial(n - 1)   # multiply AFTER return

# Tail recursive — recursive call is the last thing
def factorial_tail(n, accumulator=1):
    if n == 0:
        return accumulator
    return factorial_tail(n - 1, n * accumulator)  # passes result along

print(factorial_tail(5))   # Output: 120
```

> **Interview note:** Python does NOT optimize tail recursion (unlike Haskell, Scala). Even tail recursive functions hit the recursion limit. Mention this — it shows depth of knowledge.

---

## 8. Converting Recursion to Iteration

Any recursion can be converted to iteration using an **explicit stack**.

```python
# Recursive DFS on a graph
def dfs_recursive(graph, node, visited=None):
    if visited is None:
        visited = set()
    visited.add(node)
    print(node)
    for neighbor in graph[node]:
        if neighbor not in visited:
            dfs_recursive(graph, neighbor, visited)

# Iterative DFS — same result using explicit stack
def dfs_iterative(graph, start):
    visited = set()
    stack   = [start]

    while stack:
        node = stack.pop()
        if node not in visited:
            visited.add(node)
            print(node)
            for neighbor in graph[node]:
                if neighbor not in visited:
                    stack.append(neighbor)

graph = {
    "A": ["B", "C"],
    "B": ["D", "E"],
    "C": ["F"],
    "D": [], "E": [], "F": []
}
dfs_iterative(graph, "A")
```

---

## Quick Reference

```python
# RECURSION TEMPLATE
def recursive_func(problem):
    # 1. Base case — stop condition
    if base_condition:
        return base_result

    # 2. Reduce problem
    smaller = make_smaller(problem)

    # 3. Recursive call + combine result
    return combine(recursive_func(smaller))

# COMMON BASE CASES
if n == 0: return 0          # number problems
if n == 1: return 1          # factorial
if n <= 1: return n          # fibonacci
if len(s) == 0: return s     # string problems
if len(arr) <= 1: return arr # sorting
if left > right: return -1   # binary search

# MEMOIZATION
from functools import lru_cache
@lru_cache(maxsize=None)
def func(n): ...

# Manual memo
memo = {}
def func(n):
    if n in memo: return memo[n]
    memo[n] = compute(n)
    return memo[n]

# RECURSION LIMIT
import sys
sys.getrecursionlimit()       # 1000 default
sys.setrecursionlimit(10000)  # increase

# COMPLEXITY GUIDE
# O(n)     — linear recursion (factorial, sum)
# O(log n) — binary recursion (binary search, fast power)
# O(n²)    — quadratic (naive fibonacci without memo)
# O(2ⁿ)   — exponential (Tower of Hanoi, subsets)
# O(n log n) — divide and conquer (merge sort)
```

---

## Interview Short Answers

**Q: What is recursion and what are its two required parts?**
> Recursion is when a function calls itself to solve a smaller version of the same problem. Every recursive function needs two parts — a base case that stops the recursion and returns a direct answer, and a recursive case that calls the function with a smaller or simpler input. Without a base case the function runs forever and causes a stack overflow.

**Q: What is the call stack and how does recursion use it?**
> The call stack is a data structure Python uses to track active function calls. Each function call is pushed onto the stack. With recursion, calls stack up until the base case is reached, then each call returns and is popped off the stack in reverse order — unwinding back to the original call. Python has a default recursion limit of 1000 to prevent infinite recursion from consuming all memory.

**Q: What is the time complexity of naive recursive Fibonacci and how do you optimize it?**
> Naive recursive Fibonacci is O(2ⁿ) because the same subproblems are computed repeatedly — `fibonacci(3)` is computed many times within `fibonacci(5)`. This is optimized with memoization — caching already-computed results. Using `@lru_cache` reduces it to O(n) time and O(n) space because each subproblem is computed only once.

**Q: What is the difference between recursion and iteration?**
> Both can solve the same problems. Recursion uses the call stack implicitly and is cleaner for problems with natural recursive structure like trees, graphs, and divide-and-conquer. Iteration uses loops and is faster with O(1) space. Recursion risks stack overflow for large inputs. Any recursion can be replaced with iteration using an explicit stack.

**Q: What is memoization?**
> Memoization is an optimization technique that caches the results of expensive function calls and returns the cached result when the same inputs occur again. It converts overlapping subproblems from being recomputed to being looked up in O(1). In Python, `@functools.lru_cache` applies memoization automatically. It is the top-down approach to dynamic programming.

**Q: What is divide and conquer?**
> Divide and conquer is a recursive strategy where the problem is divided into smaller independent subproblems, each subproblem is solved recursively, and the results are combined. Classic examples are merge sort — divide array in half, sort each half, merge — and binary search — divide search space in half each step. Divide and conquer typically gives O(n log n) or O(log n) complexity.

**Q: What is Tower of Hanoi and what is its time complexity?**
> Tower of Hanoi is a classic recursion problem — move n disks from source to destination using an auxiliary peg, one disk at a time, never placing a larger disk on a smaller one. The solution requires 2ⁿ - 1 moves, making it O(2ⁿ) time complexity. It is the canonical example used to explain recursion because the solution is elegant and natural recursively but difficult to express iteratively.
