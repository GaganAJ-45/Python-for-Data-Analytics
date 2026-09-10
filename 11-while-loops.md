# While Loops in Python
> Foundation Notes — Interview Ready | DSA Focused

---

## 1. What is a While Loop?

A `while` loop repeatedly executes a block of code **as long as a condition is True**. Unlike a `for` loop which iterates over a sequence, a `while` loop runs based on a condition.

```
Check condition → True → run block → check again → True → run block → ...
                → False → exit loop
```

**Where to use:**
- When you don't know how many times to loop in advance
- Input validation — keep asking until valid input
- Game loops — keep playing until user quits
- Algorithm loops — binary search, digit extraction

---

## 2. Basic Syntax

```python
while condition:
    # body — runs as long as condition is True
```

```python
# Print 1 to 5
i = 1
while i <= 5:
    print(i)
    i += 1
# Output: 1 2 3 4 5

# Countdown
n = 5
while n > 0:
    print(n)
    n -= 1
print("Done!")
# Output: 5 4 3 2 1 Done!
```

> ⚠️ **Always update the variable inside the loop** — forgetting `i += 1` causes an infinite loop.

---

## 3. Infinite Loop

A loop that never stops — condition never becomes False.

```python
# Infinite loop — intentional
while True:
    command = input("Enter command (quit to exit): ")
    if command == "quit":
        break
    print(f"You typed: {command}")
```

```python
# Accidental infinite loop — WRONG
i = 1
while i <= 5:
    print(i)
    # forgot i += 1 — runs forever!
```

> **Where intentional infinite loops are used:** Server loops, game loops, menu systems — run forever until explicitly broken with `break`.

---

## 4. `break` — Exit the Loop Early

Stops the loop immediately regardless of the condition.

```python
# Stop when we find 5
i = 1
while i <= 10:
    if i == 5:
        print(f"Found {i}! Stopping.")
        break
    print(i)
    i += 1
# Output: 1 2 3 4 Found 5! Stopping.
```

```python
# Password validator
while True:
    password = input("Enter password: ")
    if password == "aj123":
        print("Access granted!")
        break
    print("Wrong password. Try again.")
```

---

## 5. `continue` — Skip Current Iteration

Skips the rest of the current iteration and jumps back to the condition check.

```python
# Print only odd numbers
i = 0
while i < 10:
    i += 1
    if i % 2 == 0:
        continue    # skip even numbers
    print(i)
# Output: 1 3 5 7 9
```

```python
# Skip negative numbers — sum only positives
numbers = [10, -3, 5, -7, 8, 2]
total = 0
i = 0
while i < len(numbers):
    if numbers[i] < 0:
        i += 1
        continue    # skip negatives
    total += numbers[i]
    i += 1
print(total)   # Output: 25
```

> ⚠️ **Common mistake with `continue`:** Forgetting to increment `i` before `continue` causes an infinite loop. Always update the loop variable before `continue`.

---

## 6. `pass` — Placeholder

Does nothing — used when a block is syntactically required but you have no code yet.

```python
i = 0
while i < 5:
    pass   # TODO: add logic later
    i += 1
```

---

## 7. `while-else`

The `else` block runs **only if the loop completed normally** — without hitting a `break`.

```python
# Search for a number
numbers = [10, 20, 30, 40, 50]
target  = 35
i = 0

while i < len(numbers):
    if numbers[i] == target:
        print(f"Found {target} at index {i}")
        break
    i += 1
else:
    print(f"{target} not found in the list")
# Output: 35 not found in the list
```

```python
# Prime check using while-else
num = 29
i   = 2

while i * i <= num:
    if num % i == 0:
        print("Not prime")
        break
    i += 1
else:
    print("Prime")   # runs because no break happened
# Output: Prime
```

> **Interview tip:** `while-else` is unique to Python — most languages don't have it. Mentioning it in an interview shows depth of Python knowledge. The `else` runs when the loop finishes naturally, not when `break` exits it.

---

## 8. Common While Loop Patterns

### Input Validation — keep asking until valid
```python
age = int(input("Enter your age: "))
while age < 0 or age > 120:
    print("Invalid age. Enter between 0 and 120.")
    age = int(input("Enter your age: "))
print(f"Your age is {age}")
```

### Keep asking for positive number
```python
num = int(input("Enter a positive number: "))
while num <= 0:
    num = int(input("Must be positive. Try again: "))
print(f"Got it: {num}")
```

### Sum until user enters 0
```python
total = 0
num   = int(input("Enter number (0 to stop): "))

while num != 0:
    total += num
    num = int(input("Enter number (0 to stop): "))

print(f"Total: {total}")
```

### Digit Extraction — foundation of many DSA problems
```python
num   = 12345
total = 0

while num > 0:
    digit = num % 10     # extract last digit
    total += digit
    num   = num // 10    # remove last digit

print(total)   # Output: 15  (1+2+3+4+5)
```

### Reverse a Number
```python
num = 12345
rev = 0

while num > 0:
    digit = num % 10
    rev   = rev * 10 + digit
    num   = num // 10

print(rev)   # Output: 54321
```

---

## 9. `while` vs `for` — When to Use Which

| Situation | Use |
|---|---|
| Known number of iterations | `for` |
| Iterating over a sequence | `for` |
| Unknown number of iterations | `while` |
| Loop until a condition changes | `while` |
| Input validation | `while` |
| Infinite loop with break | `while True` |
| Digit/number manipulation | `while` |

---

## 10. DSA Patterns Using While Loop

### Binary Search — O(log n)
```python
def binary_search(arr, target):
    left, right = 0, len(arr) - 1

    while left <= right:
        mid = (left + right) // 2
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1

    return -1

arr = [1, 3, 5, 7, 9, 11, 13]
print(binary_search(arr, 7))    # Output: 3
print(binary_search(arr, 6))    # Output: -1
```

### Two Pointer — O(n)
```python
# Check if array is palindrome
def is_palindrome(arr):
    left, right = 0, len(arr) - 1

    while left < right:
        if arr[left] != arr[right]:
            return False
        left  += 1
        right -= 1

    return True

print(is_palindrome([1, 2, 3, 2, 1]))   # Output: True
print(is_palindrome([1, 2, 3, 4, 5]))   # Output: False
```

### Euclidean GCD — O(log n)
```python
def gcd(a, b):
    while b:
        a, b = b, a % b
    return a

print(gcd(48, 18))   # Output: 6
```

---

## Quick Reference

```python
# BASIC
i = 0
while condition:
    body
    i += 1          # always update to avoid infinite loop

# INFINITE LOOP
while True:
    if exit_condition:
        break

# BREAK — exit loop early
while condition:
    if something:
        break

# CONTINUE — skip current iteration
while condition:
    if skip_condition:
        i += 1      # update BEFORE continue
        continue
    body
    i += 1

# WHILE-ELSE
while condition:
    if found:
        break
else:
    # runs only if no break occurred
    not_found_logic

# DIGIT EXTRACTION PATTERN
while num > 0:
    digit = num % 10    # last digit
    num   = num // 10   # remove last digit
```

---

## Interview Short Answers

**Q: What is the difference between a `while` loop and a `for` loop?**
> A `for` loop iterates over a sequence for a known number of times. A `while` loop runs as long as a condition is True — used when the number of iterations is not known in advance. For example, reading input until the user types "quit" or running a binary search are natural fits for `while` loops.

**Q: What is an infinite loop and when is it used intentionally?**
> An infinite loop runs forever because its condition never becomes False — typically `while True`. It is used intentionally for server loops, game loops, and menu systems where the program should keep running until an explicit exit condition is met using `break`.

**Q: What is the difference between `break` and `continue`?**
> `break` exits the loop entirely — no more iterations happen. `continue` skips the rest of the current iteration and jumps back to the condition check — the loop keeps running. `break` is used when you found what you were looking for. `continue` is used when you want to skip certain values but keep looping.

**Q: What is `while-else` in Python?**
> The `else` block of a `while` loop runs only when the loop condition becomes False naturally — it does NOT run if the loop was exited via `break`. This is useful for search problems where you want to run code only if the search completed without finding the target. Most languages do not have this construct — it is unique to Python.

**Q: What is the common mistake with `continue` in a while loop?**
> Forgetting to update the loop variable before `continue`. If `i += 1` comes after the `continue` statement, it is never reached, causing an infinite loop. Always place the loop variable update before the `continue` call.
