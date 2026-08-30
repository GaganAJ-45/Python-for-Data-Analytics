# Operators in Python

## What are Operators?

Operators are **special symbols** that perform operations on values and variables.

```python
result = 10 + 5   # Here '+' is the operator
#        ^   ^─── operands
#        operator
```

Python has 7 types of operators:
1. Arithmetic Operators
2. Assignment Operators
3. Comparison Operators
4. Logical Operators
5. Identity Operators
6. Membership Operators
7. Bitwise Operators

---

## 1. Arithmetic Operators

Used to perform basic **mathematical calculations**.

| Operator | Name | Example | Result |
|---|---|---|---|
| `+` | Addition | `10 + 3` | `13` |
| `-` | Subtraction | `10 - 3` | `7` |
| `*` | Multiplication | `10 * 3` | `30` |
| `/` | Division | `10 / 3` | `3.333...` |
| `//` | Floor Division | `10 // 3` | `3` |
| `%` | Modulus | `10 % 3` | `1` |
| `**` | Exponentiation | `10 ** 3` | `1000` |

**Where to use:**
- `+` `-` `*` `/` → Basic calculations, totals, averages
- `//` → Splitting items evenly (e.g. how many teams of 3 from 10 people)
- `%` → Checking even/odd, finding remainders, cycling through indexes
- `**` → Area/volume calculations, compound interest, power functions

```python
a = 10
b = 3

print(a + b)   # Output: 13
print(a - b)   # Output: 7
print(a * b)   # Output: 30
print(a / b)   # Output: 3.3333333333333335  (always returns float)
print(a // b)  # Output: 3   (removes decimal, rounds DOWN)
print(a % b)   # Output: 1   (remainder after division)
print(a ** b)  # Output: 1000

# Real use: check if a number is even or odd
number = 8
if number % 2 == 0:
    print("Even")   # Output: Even

# Real use: split people into groups
people = 10
group_size = 3
print(people // group_size)  # Output: 3 (complete groups)
print(people % group_size)   # Output: 1 (leftover people)
```

### ⚠️ Gotcha — Floor Division and Modulus with Negative Numbers

```python
# Floor division rounds toward NEGATIVE INFINITY (not toward zero)
print(-7 // 2)    # Output: -4  (NOT -3!)
print(-7 % 2)     # Output: 1   (Python % result always has the sign of the divisor)

print(7 // -2)    # Output: -4
print(7 % -2)     # Output: -1

# Exponentiation binds tighter than unary minus
print(-2 ** 2)    # Output: -4  (evaluated as -(2**2), NOT (-2)**2)
print((-2) ** 2)  # Output: 4   (use parentheses to be explicit)
```

---

## 2. Assignment Operators

Used to **assign values to variables**. The basic one is `=`. Compound operators combine arithmetic with assignment in one step.

| Operator | Meaning | Example | Equivalent to |
|---|---|---|---|
| `=` | Assign | `x = 5` | `x = 5` |
| `+=` | Add and assign | `x += 3` | `x = x + 3` |
| `-=` | Subtract and assign | `x -= 2` | `x = x - 2` |
| `*=` | Multiply and assign | `x *= 4` | `x = x * 4` |
| `/=` | Divide and assign | `x /= 6` | `x = x / 6` |
| `%=` | Modulus and assign | `x %= 3` | `x = x % 3` |
| `**=` | Exponent and assign | `x **= 2` | `x = x ** 2` |
| `//=` | Floor div and assign | `x //= 3` | `x = x // 3` |

**Where to use:**
- `=` → Storing any value in a variable
- `+=` → Incrementing counters, accumulating totals in loops
- `-=` → Countdown timers, decreasing stock/inventory
- `*=` → Scaling values, applying multipliers
- `/=` → Averaging, normalizing values
- `**=` → Repeated squaring, power calculations
- `//=` → Integer division in place, pagination logic

```python
x = 5

x += 3         # x = x + 3 → x is now 8
print(x)       # Output: 8

x -= 2         # x = x - 2 → x is now 6
print(x)       # Output: 6

x *= 4         # x = x * 4 → x is now 24
print(x)       # Output: 24

x /= 6         # x = x / 6 → x is now 4.0
print(x)       # Output: 4.0

x = 3
x **= 2        # x = x ** 2 → x is now 9
print(x)       # Output: 9

x //= 2        # x = x // 2 → x is now 4
print(x)       # Output: 4

# Real use: accumulating a total in a loop
total = 0
prices = [10, 25, 5, 40]
for price in prices:
    total += price
print(total)   # Output: 80

# Real use: counter
count = 0
for item in ["a", "b", "c"]:
    count += 1
print(count)   # Output: 3
```

### ⚠️ Gotcha — `+=` behaves differently on mutable vs immutable objects

```python
# With a LIST (mutable) — += modifies the SAME object in place
a = [1, 2, 3]
b = a           # b points to the same list as a
a += [4]
print(a)        # Output: [1, 2, 3, 4]
print(b)        # Output: [1, 2, 3, 4]  ← b changed too! (same object)

# With an INT (immutable) — += creates a NEW object
x = 5
y = x           # y points to the same int as x
x += 1
print(x)        # Output: 6
print(y)        # Output: 5  ← y is unaffected (new object was created for x)
```

> **Why this matters:** Mutable types (list, dict, set) share references. Immutable types
> (int, float, str, tuple) always create a new object on reassignment. This is a very
> common interview question.

---

## 3. Comparison Operators

Used to **compare two values**. Always return `True` or `False`.

| Operator | Meaning | Example | Result |
|---|---|---|---|
| `==` | Equal to | `10 == 10` | `True` |
| `!=` | Not equal to | `10 != 20` | `True` |
| `>` | Greater than | `10 > 5` | `True` |
| `<` | Less than | `10 < 5` | `False` |
| `>=` | Greater than or equal | `10 >= 10` | `True` |
| `<=` | Less than or equal | `10 <= 25` | `True` |

**Where to use:**
- `==` → Checking passwords, matching user input
- `!=` → Filtering out unwanted values
- `>` `<` → Sorting logic, finding max/min manually
- `>=` `<=` → Age validation, score thresholds, range checks

```python
a = 10
b = 20

print(a == b)    # Output: False
print(a != b)    # Output: True
print(a > b)     # Output: False
print(a < b)     # Output: True
print(a >= 10)   # Output: True
print(b <= 25)   # Output: True

# Real use: grade check
marks = 85
if marks >= 90:
    print("Grade A")
elif marks >= 75:
    print("Grade B")   # Output: Grade B
else:
    print("Grade C")
```

### ⚠️ Gotcha — Chained Comparisons and Type Comparisons

```python
# Python supports chaining — much cleaner than writing two conditions
x = 5
print(1 < x < 10)     # Output: True  (same as: 1 < x and x < 10)
print(10 < x < 1)     # Output: False

# == compares value, not type
print(5 == 5.0)        # Output: True  (same numeric value, different types)
print(5 == "5")        # Output: False (int vs string — no implicit conversion)
```

---

## 4. Logical Operators

Used to **combine multiple conditions**. Return `True` or `False`.

| Operator | Meaning | Returns True when... |
|---|---|---|
| `and` | Both conditions | Both sides are True |
| `or` | Either condition | At least one side is True |
| `not` | Reverse condition | The condition is False |

**Where to use:**
- `and` → Login validation (correct username AND password)
- `or` → Flexible filters (search for this OR that)
- `not` → Toggling flags, reversing a condition

```python
x = 5
y = 10
z = 15

# and — BOTH must be True
print(x > 0 and y > 5)     # Output: True
print(x > 0 and y > 20)    # Output: False  (second condition fails)

# or — AT LEAST ONE must be True
print(x > 10 or z > 10)    # Output: True   (z > 10 is True)
print(x > 10 or y > 20)    # Output: False  (both fail)

# not — REVERSES the result
print(not(x > 10))          # Output: True   (x > 10 is False, not flips it)
print(not(x > 0))           # Output: False  (x > 0 is True, not flips it)

# Real use: login check
username = "aj"
password = "1234"
if username == "aj" and password == "1234":
    print("Login successful")   # Output: Login successful
```

### ⚠️ Gotcha — `and`/`or` return a VALUE, not just True/False (Short-circuit evaluation)

```python
# and: returns the FIRST falsy value, or the LAST value if all are truthy
print(5 and 10)      # Output: 10  (both truthy → returns last operand)
print(0 and 10)      # Output: 0   (0 is falsy → stops and returns 0)

# or: returns the FIRST truthy value, or the LAST value if all are falsy
print(5 or 10)       # Output: 5   (5 is truthy → stops immediately, returns 5)
print(0 or 10)       # Output: 10  (0 is falsy → moves to next, returns 10)
print(0 or "")       # Output: ""  (both falsy → returns last one)

# Real use: default value pattern
name = None
display_name = name or "Guest"
print(display_name)  # Output: Guest
```

> **Short-circuit** means Python stops evaluating as soon as the result is determined.
> `0 and anything` → Python already knows result is False, skips the second part.
> `5 or anything` → Python already knows result is True, skips the second part.
> This is used to write efficient, cleaner conditions.

---

## 5. Identity Operators

Used to check whether two variables **point to the same object in memory** — not just equal values.

| Operator | Meaning |
|---|---|
| `is` | True if both variables are the SAME object in memory |
| `is not` | True if both variables are DIFFERENT objects in memory |

**Where to use:**
- `is None` → The standard way to check if a variable has no value
- `is not None` → Check if something was actually assigned
- **Never use `is` to compare values like numbers or strings**

```python
a = [1, 2, 3]
b = [1, 2, 3]   # Same content, but a different object
c = a           # c points to the exact same object as a

print(a == b)   # Output: True   (same values)
print(a is b)   # Output: False  (different objects in memory)
print(a is c)   # Output: True   (same object — c is just another name for a)

print(id(a))    # e.g. 140234...
print(id(b))    # different id
print(id(c))    # same id as a

# Correct use of 'is'
value = None
if value is None:
    print("No value assigned")   # Output: No value assigned
```

### ⚠️ Gotcha 1 — Small Integer Caching (-5 to 256)

```python
x = 100
y = 100
print(x is y)    # Output: True  (same cached object — always)

x = 1000
y = 1000
print(x is y)    # Output: False in REPL / True inside a .py script
```

> ⚠️ This output is **environment-dependent**:
> - In the **interactive shell (REPL)** → `False` for large integers
> - Inside a **.py script** → often `True` (CPython reuses same literal objects)
> Always use `==` to compare values. Never rely on `is` for numbers.

### ⚠️ Gotcha 2 — String Interning

```python
s1 = "hello"
s2 = "hello"
print(s1 is s2)     # Output: True  (short strings interned/reused)

s3 = "hello world!"
s4 = "hello world!"
print(s3 is s4)     # Output: False in REPL / may be True inside .py script
```

> ⚠️ Same environment-dependent behavior. Never rely on `is` for strings.

**Golden rule:** Use `==` for value comparison. Use `is` only for `None`.

---

## 6. Membership Operators

Used to check whether a value **exists inside a sequence** (list, string, tuple, dict, set).

| Operator | Meaning |
|---|---|
| `in` | True if value IS found in the sequence |
| `not in` | True if value is NOT found in the sequence |

**Where to use:**
- Checking if a username exists in a list of users
- Searching for a word in a sentence
- Validating allowed values (e.g. allowed file types)
- Checking keys in a dictionary

```python
my_list = [1, 2, 3, 4, 5]
my_string = "Python"

print(3 in my_list)          # Output: True
print(6 not in my_list)      # Output: True
print("P" in my_string)      # Output: True
print("z" not in my_string)  # Output: True

# Real use: word search
sentence = "Python is fun"
if "Python" in sentence:
    print("Found it!")       # Output: Found it!
```

### ⚠️ Gotcha — `in` with Dictionaries checks KEYS, not values

```python
my_dict = {"name": "AJ", "role": "Developer"}

print("name" in my_dict)          # Output: True  (checks KEYS)
print("AJ" in my_dict)            # Output: False ("AJ" is a value, not a key)
print("AJ" in my_dict.values())   # Output: True  (explicitly check values)
print("name" in my_dict.keys())   # Output: True  (same as default behavior)
```

---

## 7. Bitwise Operators

Operate directly on **binary (bit-level) representations** of integers.

| Operator | Name | Example | Result |
|---|---|---|---|
| `&` | AND | `5 & 3` | `1` |
| `\|` | OR | `5 \| 3` | `7` |
| `^` | XOR | `5 ^ 3` | `6` |
| `~` | NOT | `~5` | `-6` |
| `<<` | Left Shift | `5 << 1` | `10` |
| `>>` | Right Shift | `5 >> 1` | `2` |

**Where to use:**
- `&` → Checking flags/permissions, checking even/odd
- `|` → Setting flags/permissions
- `^` → Toggling bits, swapping values without temp variable
- `~` → Inverting bits (masking operations)
- `<<` `>>` → Fast multiply/divide by powers of 2

### How it works (binary breakdown):

```
a = 5  →  binary: 101
b = 3  →  binary: 011

& (AND)  → both bits must be 1    →  101 & 011 = 001 = 1
| (OR)   → at least one bit is 1  →  101 | 011 = 111 = 7
^ (XOR)  → bits must be different →  101 ^ 011 = 110 = 6
~ (NOT)  → flips all bits         →  ~5 = -(5+1) = -6
<< 1     → shift left by 1        →  101 becomes 1010 = 10  (like x * 2)
>> 1     → shift right by 1       →  101 becomes 010  = 2   (like x // 2)
```

```python
a = 5   # binary: 101
b = 3   # binary: 011

print(a & b)    # Output: 1   (AND)
print(a | b)    # Output: 7   (OR)
print(a ^ b)    # Output: 6   (XOR)
print(~a)       # Output: -6  (NOT — formula: -(n+1))
print(a << 1)   # Output: 10  (left shift — multiply by 2)
print(a >> 1)   # Output: 2   (right shift — divide by 2)
```

### ⚠️ Gotcha — Common Bitwise Tricks Asked in Interviews

```python
# 1. Check even or odd using & (faster than %)
n = 7
print(n & 1)     # Output: 1 → odd  (last bit is 1)
n = 8
print(n & 1)     # Output: 0 → even (last bit is 0)

# 2. Swap two numbers WITHOUT a temp variable using XOR
a, b = 5, 9
a = a ^ b
b = a ^ b
a = a ^ b
print(a, b)      # Output: 9 5

# 3. Fast multiply/divide by powers of 2
print(5 << 1)    # Output: 10   same as 5 * 2
print(5 << 2)    # Output: 20   same as 5 * 4
print(20 >> 2)   # Output: 5    same as 20 // 4
```

---

## 8. Walrus Operator `:=` (Python 3.8+)

The walrus operator **assigns a value AND returns it** in a single expression. It lets you assign inside conditions, loops, and comprehensions.

**Where to use:** Avoiding double evaluation — when you need to use a computed value both in a condition and inside the block.

```python
# Without walrus — computing len() twice
data = [1, 2, 3, 4, 5]
if len(data) > 3:
    print(f"List is long: {len(data)} items")   # len() called twice

# With walrus — compute once, reuse
if (n := len(data)) > 3:
    print(f"List is long: {n} items")   # Output: List is long: 5 items
#    ^^ assigns len(data) to n AND checks if > 3

# Real use: reading input until user types "quit"
while (user_input := input("Enter command: ")) != "quit":
    print(f"You typed: {user_input}")

# Real use: in a while loop with a computed condition
import random
while (num := random.randint(1, 10)) != 5:
    print(f"Got {num}, trying again...")
print("Got 5!")
```

> **Interview tip:** The walrus operator `:=` is called the walrus operator because `:=` looks like the eyes and tusks of a walrus. It was introduced in Python 3.8. Use it to make code cleaner when you need to assign and check a value at the same time.

---

## Quick Reference — All Operators

```python
# ARITHMETIC
+    # Addition
-    # Subtraction
*    # Multiplication
/    # Division (always float)
//   # Floor division (rounds down)
%    # Modulus (remainder)
**   # Exponentiation (power)

# ASSIGNMENT
=    # Assign
+=   # Add and assign
-=   # Subtract and assign
*=   # Multiply and assign
/=   # Divide and assign
%=   # Modulus and assign
**=  # Exponent and assign
//=  # Floor divide and assign
:=   # Walrus — assign and return (Python 3.8+)

# COMPARISON (always return True or False)
==   # Equal to
!=   # Not equal to
>    # Greater than
<    # Less than
>=   # Greater than or equal to
<=   # Less than or equal to

# LOGICAL
and  # Both conditions must be True
or   # At least one condition must be True
not  # Reverses the result

# IDENTITY
is       # Same object in memory
is not   # Different objects in memory

# MEMBERSHIP
in       # Value exists in sequence
not in   # Value does not exist in sequence

# BITWISE
&    # AND
|    # OR
^    # XOR
~    # NOT (flips bits)
<<   # Left shift (multiply by 2^n)
>>   # Right shift (divide by 2^n)
```

---

## Operator Precedence (High to Low)

```
1.  ()            → Parentheses (highest priority)
2.  **            → Exponentiation
3.  ~             → Bitwise NOT
4.  * / // %      → Multiplication, Division, Floor Div, Modulus
5.  + -           → Addition, Subtraction
6.  << >>         → Bitwise Shifts
7.  &             → Bitwise AND
8.  ^             → Bitwise XOR
9.  |             → Bitwise OR
10. == != > < >= <=  → Comparisons
11. is / is not      → Identity
12. in / not in      → Membership
13. not           → Logical NOT
14. and           → Logical AND
15. or            → Logical OR (lowest priority)
```

```python
print(2 + 3 * 4)        # Output: 14   (* before +)
print((2 + 3) * 4)      # Output: 20   (parentheses first)
print(2 ** 3 ** 2)      # Output: 512  (** is right-associative: 3**2=9, 2**9=512)
print(True and 5 > 3)   # Output: True (> before and)
```

---

## Interview Short Answers

**Q: What is the difference between `/` and `//`?**
> `/` always returns a float — even if both operands are integers (`10 / 2` gives `5.0`). `//` is floor division — it divides and rounds down to the nearest integer (`10 // 3` gives `3`, `-7 // 2` gives `-4` not `-3`).

**Q: What is short-circuit evaluation?**
> Python stops evaluating a logical expression as soon as the result is determined. With `and`, if the first operand is falsy, Python returns it immediately without checking the second. With `or`, if the first operand is truthy, Python returns it immediately. This is used for default values: `name = user_input or "Guest"`.

**Q: What does `and`/`or` actually return?**
> They don't always return `True` or `False` — they return one of the operands. `and` returns the first falsy value, or the last value if all are truthy. `or` returns the first truthy value, or the last value if all are falsy. For example, `5 and 10` returns `10`, and `0 or "hello"` returns `"hello"`.

**Q: What is the walrus operator?**
> The walrus operator `:=` was introduced in Python 3.8. It assigns a value to a variable and returns it in the same expression. It is useful when you need to compute a value, check it in a condition, and use it inside the block — avoiding computing it twice.

**Q: What is the difference between `==` and `is`?**
> `==` compares values — checks if two objects contain the same data. `is` compares identity — checks if two variables point to the exact same object in memory. Always use `==` for value comparison. Only use `is` to check against `None`.

**Q: How do you check if a number is even using bitwise operators?**
> Use `n & 1`. If the result is `0`, the number is even. If it is `1`, the number is odd. This works because the last bit of any even number in binary is always `0`, and the last bit of any odd number is always `1`.
