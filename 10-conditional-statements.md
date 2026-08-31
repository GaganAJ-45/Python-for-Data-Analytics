# Conditional Statements in Python

## What are Conditional Statements?

Conditional statements allow your program to **make decisions** — execute different blocks of code based on whether a condition is `True` or `False`.

```
Condition True  → execute this block
Condition False → execute that block
```

Python has three conditional keywords:
- `if` — check a condition
- `elif` — check another condition if previous was False
- `else` — run if no condition was True

---

## 1. The `if` Statement

Execute a block **only if** the condition is `True`.

**Syntax:**
```python
if condition:
    # runs only when condition is True
```

```python
time = 20   # 8 PM in 24-hour format

if time == 20:
    print("It's time for dinner!")
# Output: It's time for dinner!
```

```python
age = 20
if age >= 18:
    print("Eligible to vote")
    print("Remember to bring your voter ID")
# Both lines run — both belong to the if block (indented)
```

---

## 2. The `else` Statement

Provides an **alternative block** when the `if` condition is `False`.

**Syntax:**
```python
if condition:
    # runs when True
else:
    # runs when False
```

```python
time = 18   # 6 PM

if time == 20:
    print("It's dinner time!")
else:
    print("It's not dinner time yet.")
# Output: It's not dinner time yet.
```

```python
age = 16
if age >= 18:
    print("Eligible to vote")
else:
    print("Not eligible to vote")
# Output: Not eligible to vote
```

---

## 3. The `elif` Statement

Check **another condition** if the previous one was `False`. You can chain as many `elif` blocks as needed.

**Syntax:**
```python
if condition1:
    # runs if condition1 is True
elif condition2:
    # runs if condition2 is True
elif condition3:
    # runs if condition3 is True
else:
    # runs if none were True
```

```python
time = 15   # 3 PM

if time == 8:
    print("Breakfast time!")
elif time == 13:
    print("Lunch time!")
elif time == 20:
    print("Dinner time!")
else:
    print("Not a meal time.")
# Output: Not a meal time.
```

> **Important:** Python checks conditions **top to bottom** and stops at the **first True** condition. Remaining `elif` and `else` blocks are skipped.

---

## 4. Real-World Examples

### KSRTC Bus Ticket Pricing
```python
age = 65

if age < 5:
    print("Ticket is free")
elif age <= 12:
    print("Child discount applied")
elif age >= 60:
    print("Senior citizen discount applied")
else:
    print("Full fare")
# Output: Senior citizen discount applied
```

### Grade Calculator
```python
marks = 85

if marks >= 90:
    print("Grade A — Distinction")
elif marks >= 80:
    print("Grade B — First Class")
elif marks >= 70:
    print("Grade C — Second Class")
elif marks >= 50:
    print("Grade D — Pass")
else:
    print("Grade F — Fail")
# Output: Grade B — First Class
```

### Check Positive, Negative, or Zero
```python
num = int(input("Enter a number: "))

if num > 0:
    print("Positive")
elif num < 0:
    print("Negative")
else:
    print("Zero")
```

---

## 5. Logical Operators in Conditions

Combine multiple conditions using `and`, `or`, `not`.

```python
# and — BOTH must be True
age = 16
has_student_id = True

if age < 18 and has_student_id:
    print("Eligible for student discount")
# Output: Eligible for student discount

# or — AT LEAST ONE must be True
day = "Saturday"
if day == "Saturday" or day == "Sunday":
    print("It's the weekend!")
# Output: It's the weekend!

# not — REVERSES the condition
is_raining = False
if not is_raining:
    print("Good day to go out!")
# Output: Good day to go out!
```

### Safe Chaining with Short-Circuit Evaluation
```python
# Short-circuit prevents error — if name is empty, second check is skipped
name = ""
if name and name.startswith("A"):
    print(f"Name starts with A: {name}")
else:
    print("No valid name")
# Output: No valid name
# If name="" (falsy), Python skips name.startswith("A") entirely
```

---

## 6. Nested `if` Statements

An `if` inside another `if` — use when decisions depend on multiple levels.

```python
day = "Saturday"
is_raining = False

if day == "Saturday" or day == "Sunday":
    if not is_raining:
        print("Let's visit Mysuru!")
    else:
        print("It's raining, let's stay home.")
else:
    print("It's a weekday, wait for the weekend.")
# Output: Let's visit Mysuru!
```

### Banking System — Nested Conditions
```python
account_num = 123456789
pin         = 4522
balance     = 50000

acc_input = int(input("Account number: "))
pin_input = int(input("PIN: "))
withdraw  = int(input("Amount to withdraw: "))

if acc_input == account_num:
    if pin_input == pin:
        if withdraw > balance:
            print("Insufficient balance")
        elif withdraw <= 0:
            print("Invalid amount")
        else:
            balance -= withdraw
            print(f"Withdrawn ₹{withdraw}. Balance: ₹{balance}")
    else:
        print("Incorrect PIN")
else:
    print("Account not found")
```

> **Interview tip:** Deeply nested `if` statements (3+ levels) are a code smell. Try to flatten them using `and`/`or` or early returns in functions.

---

## 7. Indentation in Python

Python uses **indentation** (4 spaces) to define code blocks — NOT curly braces like Java/C.

```python
age = 20

if age >= 18:
    print("Adult")         # inside if block
    print("Can vote")      # also inside if block
print("Program ends")      # outside if block — always runs
```

```python
# Wrong indentation — IndentationError
if age >= 18:
print("Adult")    # ❌ IndentationError — must be indented
```

> **Rule:** Everything at the same indentation level belongs to the same block. Python is strict about this — mixing tabs and spaces causes `TabError`.

---

## 8. Truthy and Falsy in Conditions

Any value can be used directly in an `if` condition — Python evaluates its truthiness.

**Falsy values** — evaluate to `False`:
```python
if 0:        print("runs")   # ❌ won't run — 0 is falsy
if "":       print("runs")   # ❌ won't run — empty string is falsy
if []:       print("runs")   # ❌ won't run — empty list is falsy
if None:     print("runs")   # ❌ won't run — None is falsy
```

**Truthy values** — everything else:
```python
if 1:        print("runs")   # ✅ runs
if "hello":  print("runs")   # ✅ runs
if [1, 2]:   print("runs")   # ✅ runs
```

**Real use — checking if a list or string has content:**
```python
name = input("Enter name: ")
if name:                      # cleaner than: if name != ""
    print(f"Hello {name}")
else:
    print("No name entered")

cart = []
if not cart:                  # cleaner than: if len(cart) == 0
    print("Your cart is empty")
```

---

## 9. Ternary Operator — One-Line `if-else`

Assign a value based on a condition in one line.

**Syntax:**
```python
value = result_if_true if condition else result_if_false
```

```python
# Traditional
num = 10
if num % 2 == 0:
    result = "even"
else:
    result = "odd"

# Ternary — same in one line
result = "even" if num % 2 == 0 else "odd"
print(result)   # Output: even

# More examples
age    = 20
status = "adult" if age >= 18 else "minor"
print(status)   # Output: adult

# In print directly
num = 15
print("Positive" if num > 0 else "Non-positive")   # Output: Positive

# In a list comprehension
numbers = [1, -2, 3, -4, 5]
labels  = ["pos" if n > 0 else "neg" for n in numbers]
print(labels)   # Output: ['pos', 'neg', 'pos', 'neg', 'pos']
```

> **Interview tip:** Ternary is clean for simple conditions. Don't use it for complex logic — it hurts readability.

---

## 10. The `pass` Statement

`pass` is a **placeholder** — does nothing but prevents a syntax error when a block is required but you have no code to put there yet.

```python
age = 20

if age >= 18:
    pass    # TODO: add voting logic later
else:
    print("Not eligible")

# Also used in empty functions/classes during development
def process_data():
    pass    # implement later
```

---

## 11. `match-case` Statement (Python 3.10+)

Pattern matching — cleaner alternative to long `if-elif` chains when checking one variable against multiple values. Similar to `switch-case` in C/Java.

**Syntax:**
```python
match variable:
    case value1:
        # code
    case value2:
        # code
    case _:
        # default (like else)
```

```python
day = "Sunday"

match day:
    case "Monday":
        print("Start of work week")
    case "Friday":
        print("Almost weekend!")
    case "Saturday" | "Sunday":    # | means OR — matches either value
        print("It's the weekend!")
    case _:
        print("Just another weekday")
# Output: It's the weekend!
```

### Guard Conditions in `match-case`
Add an extra condition using `if` inside a case:

```python
num = 15

match num:
    case x if x < 0:
        print("Negative")
    case x if x == 0:
        print("Zero")
    case x if x % 2 == 0:
        print("Positive even")
    case x:
        print("Positive odd")
# Output: Positive odd
```

### Matching Data Types and Structures
```python
point = (0, 5)

match point:
    case (0, 0):
        print("Origin")
    case (0, y):
        print(f"On Y-axis at y={y}")
    case (x, 0):
        print(f"On X-axis at x={x}")
    case (x, y):
        print(f"Point at ({x}, {y})")
# Output: On Y-axis at y=5
```

> **When to use `match-case` vs `if-elif`:**
> - Use `match-case` when checking **one variable** against **multiple fixed values**
> - Use `if-elif` when conditions involve **multiple variables** or **complex expressions**

---

## 12. Common Patterns in Interviews

### Input Validation Pattern
```python
age = int(input("Enter age: "))

if age < 0:
    print("Invalid — age cannot be negative")
elif age < 18:
    print("Minor")
elif age < 60:
    print("Adult")
else:
    print("Senior citizen")
```

### Check Divisibility (FizzBuzz — most asked interview question)
```python
for num in range(1, 21):
    if num % 3 == 0 and num % 5 == 0:
        print("FizzBuzz")
    elif num % 3 == 0:
        print("Fizz")
    elif num % 5 == 0:
        print("Buzz")
    else:
        print(num)
```

> **FizzBuzz is literally the most common first-round interview question.** Know it cold.

### Login System Pattern
```python
username = input("Username: ")
password = input("Password: ")

correct_user = "aj_kumar"
correct_pass = "secure123"

if username == correct_user and password == correct_pass:
    print("Login successful")
elif username != correct_user:
    print("Invalid username")
else:
    print("Incorrect password")
```

---

## Quick Reference

```python
# Basic if
if condition:
    code

# if-else
if condition:
    code
else:
    code

# if-elif-else
if condition1:
    code
elif condition2:
    code
else:
    code

# Ternary
value = x if condition else y

# Nested
if condition1:
    if condition2:
        code

# Truthy check
if variable:          # True if non-empty, non-zero, not None
if not variable:      # True if empty, zero, or None

# pass placeholder
if condition:
    pass

# match-case (Python 3.10+)
match variable:
    case value1:
        code
    case value2 | value3:    # OR pattern
        code
    case x if x > 0:         # guard condition
        code
    case _:                  # default
        code
```

---

## Interview Short Answers

**Q: What is the difference between `if-elif-else` and multiple `if` statements?**
> With `if-elif-else`, Python stops checking as soon as one condition is `True` — only one block runs. With multiple separate `if` statements, Python checks every condition independently — multiple blocks can run. Use `if-elif-else` when conditions are mutually exclusive, and separate `if` statements when each condition is independent.

**Q: What is a ternary operator in Python?**
> Python's ternary operator is written as `value = x if condition else y`. It assigns `x` if the condition is `True`, otherwise `y`. It is a one-line alternative to a simple `if-else` assignment. For example, `result = "even" if num % 2 == 0 else "odd"`.

**Q: What does `pass` do in Python?**
> `pass` is a null statement — it does nothing. It is used as a placeholder when a code block is syntactically required but you have no logic to put there yet. For example, inside an empty `if` block or a function you plan to implement later.

**Q: What is `match-case` in Python?**
> `match-case` is Python's pattern matching statement introduced in Python 3.10. It checks a variable against multiple patterns and runs the matching block. The `_` wildcard acts as a default case. It is similar to `switch-case` in C or Java but more powerful — it supports OR patterns with `|`, guard conditions with `if`, and structural pattern matching.

**Q: What is FizzBuzz?**
> FizzBuzz is a classic programming interview problem. Print numbers from 1 to N, but print "Fizz" for multiples of 3, "Buzz" for multiples of 5, and "FizzBuzz" for multiples of both. The key insight is to check `num % 3 == 0 and num % 5 == 0` first — before the individual checks — otherwise numbers like 15 would incorrectly print "Fizz" instead of "FizzBuzz".

**Q: What does Python use for indentation and why does it matter?**
> Python uses 4 spaces for indentation to define code blocks — unlike Java or C which use curly braces. Indentation is not just style in Python — it is syntax. Incorrect indentation raises an `IndentationError` or `TabError`. Mixing tabs and spaces is not allowed.
