# Number Systems and Type Conversion in Python

## 1. Numeric Data Types in Python

Python has three built-in numeric types:

```
Numeric Types
 ├── int     → whole numbers (no decimal)
 ├── float   → numbers with decimal point
 └── complex → numbers with real and imaginary parts
```

```python
a = 89          # int
b = 3.14        # float
c = 3 + 4j      # complex

print(type(a))  # Output: <class 'int'>
print(type(b))  # Output: <class 'float'>
print(type(c))  # Output: <class 'complex'>

# Check class directly
print(a.__class__)  # Output: <class 'int'>
```

### 1.1 `int`
Whole numbers — positive, negative, or zero. No size limit in Python (unlike C/Java).

```python
x = 89
y = -45
z = 0
big = 999999999999999999999   # Python handles large ints natively
```

### 1.2 `float`
Numbers with a decimal point. Stored as 64-bit double precision internally.

```python
price = 99.99
temperature = -2.5
pi = 3.14159

# Scientific notation
speed = 3e8       # 3 × 10⁸ = 300000000.0
small = 1.5e-3    # 0.0015

print(type(speed))  # Output: <class 'float'>
```

> ⚠️ **Interview gotcha:** Floating point is not always exact.
> ```python
> print(0.1 + 0.2)        # Output: 0.30000000000000004
> print(0.1 + 0.2 == 0.3) # Output: False
> ```
> This is a floating point precision issue — stored in binary, not decimal.
> Use `round()` or the `decimal` module when precision matters.

### 1.3 `complex`
Numbers with a real part and imaginary part (suffix `j`).

```python
z = 3 + 4j
print(z.real)   # Output: 3.0
print(z.imag)   # Output: 4.0
print(type(z))  # Output: <class 'complex'>
```

Used in signal processing, scientific computing, and mathematics.

---

## 2. Number Systems

Python supports four number systems:

| System | Base | Digits Used | Python Prefix |
|---|---|---|---|
| Decimal | 10 | 0–9 | (none) |
| Binary | 2 | 0, 1 | `0b` |
| Octal | 8 | 0–7 | `0o` |
| Hexadecimal | 16 | 0–9, A–F | `0x` |

```python
dec_num = 89          # Decimal  (base 10)
bin_num = 0b1011001   # Binary   (base 2)
oct_num = 0o131       # Octal    (base 8)
hex_num = 0x59        # Hex      (base 16)

# All represent the same number — 89
print(dec_num, bin_num, oct_num, hex_num)
# Output: 89 89 89 89
```

---

## 3. Python Built-in Conversion Functions

### Decimal → Other bases

```python
num = 89

print(bin(num))   # Output: 0b1011001  (binary)
print(oct(num))   # Output: 0o131      (octal)
print(hex(num))   # Output: 0x59       (hexadecimal)

# The prefix (0b, 0o, 0x) is included in the output string
# To get just the number without prefix:
print(bin(num)[2:])   # Output: 1011001
print(oct(num)[2:])   # Output: 131
print(hex(num)[2:])   # Output: 59
```

### Other bases → Decimal using `int(value, base)`

The `base` argument tells Python which number system the string is in:

```python
print(int('1011001', 2))   # Binary  → Decimal: 89
print(int('131', 8))       # Octal   → Decimal: 89
print(int('59', 16))       # Hex     → Decimal: 89

# Without base argument — treats string as decimal
print(int('89'))            # Output: 89
```

---

## 4. Manual Conversion — Decimal to Other Bases

### 4.1 Decimal to Binary
Repeatedly divide by **2**, record remainders. Read **bottom to top**.

**Example: Convert 89 to binary**

| Step | Division | Quotient | Remainder |
|---|---|---|---|
| 1 | 89 ÷ 2 | 44 | **1** |
| 2 | 44 ÷ 2 | 22 | **0** |
| 3 | 22 ÷ 2 | 11 | **0** |
| 4 | 11 ÷ 2 | 5  | **1** |
| 5 | 5 ÷ 2  | 2  | **1** |
| 6 | 2 ÷ 2  | 1  | **0** |
| 7 | 1 ÷ 2  | 0  | **1** |

Reading remainders **bottom to top → 1011001**

**89 in decimal = 1011001 in binary**

Verify: `bin(89)` → `0b1011001` ✅

---

### 4.2 Decimal to Octal
Repeatedly divide by **8**, record remainders. Read **bottom to top**.

**Example: Convert 89 to octal**

| Step | Division | Quotient | Remainder |
|---|---|---|---|
| 1 | 89 ÷ 8 | 11 | **1** |
| 2 | 11 ÷ 8 | 1  | **3** |
| 3 | 1 ÷ 8  | 0  | **1** |

Reading remainders **bottom to top → 131**

**89 in decimal = 131 in octal**

Verify: `oct(89)` → `0o131` ✅

---

### 4.3 Decimal to Hexadecimal
Repeatedly divide by **16**. If remainder > 9, use hex letters (10=A, 11=B, 12=C, 13=D, 14=E, 15=F).

**Example: Convert 89 to hexadecimal**

| Step | Division | Quotient | Remainder |
|---|---|---|---|
| 1 | 89 ÷ 16 | 5 | **9** |
| 2 | 5 ÷ 16  | 0 | **5** |

Reading remainders **bottom to top → 59**

**89 in decimal = 59 in hexadecimal**

Verify: `hex(89)` → `0x59` ✅

---

## 5. Manual Conversion — Other Bases to Decimal

### 5.1 Binary to Decimal
Multiply each digit by **2 raised to its position** (right to left starting from 0), then sum.

**Example: Convert 1011001₂ to decimal**

```
Position:  6    5    4    3    2    1    0
Digit:     1    0    1    1    0    0    1

(1 × 2⁶) = 64
(0 × 2⁵) = 0
(1 × 2⁴) = 16
(1 × 2³) = 8
(0 × 2²) = 0
(0 × 2¹) = 0
(1 × 2⁰) = 1
─────────────
Sum       = 89
```

**1011001₂ → 89** ✅

---

### 5.2 Octal to Decimal
Multiply each digit by **8 raised to its position**, then sum.

**Example: Convert 131₈ to decimal**

```
(1 × 8²) = 64
(3 × 8¹) = 24
(1 × 8⁰) = 1
─────────────
Sum       = 89
```

**131₈ → 89** ✅

---

### 5.3 Hexadecimal to Decimal
Multiply each digit by **16 raised to its position**, then sum.

**Example: Convert 59₁₆ to decimal**

```
(5 × 16¹) = 80
(9 × 16⁰) = 9
─────────────
Sum        = 89
```

**59₁₆ → 89** ✅

---

## 6. Type Conversion

Type conversion means **changing a value from one data type to another**.

There are two types:

```
Type Conversion
 ├── Implicit  → Python does it automatically
 └── Explicit  → You do it manually (Type Casting)
```

---

### 6.1 Implicit Type Conversion
Python **automatically converts** one type to another when needed — always converts to the **wider** type to avoid data loss.

```python
a = 10      # int
b = 3.5     # float

result = a + b
print(result)        # Output: 13.5
print(type(result))  # Output: <class 'float'>
# int was automatically promoted to float
```

**Conversion hierarchy (narrow → wide):**
```
bool → int → float → complex
```

```python
print(True + 5)       # Output: 6      (bool → int)
print(5 + 2.0)        # Output: 7.0    (int → float)
print(5 + (2 + 0j))   # Output: (7+0j) (int → complex)
```

> Python never implicitly converts between `str` and numeric types — that always raises a `TypeError`.
> ```python
> print("5" + 5)   # TypeError: can only concatenate str (not "int") to str
> ```

---

### 6.2 Explicit Type Conversion (Type Casting)
You manually convert using built-in functions.

| Function | Converts to | Example | Output |
|---|---|---|---|
| `int()` | Integer | `int(3.9)` | `3` |
| `float()` | Float | `float(5)` | `5.0` |
| `str()` | String | `str(89)` | `'89'` |
| `bool()` | Boolean | `bool(0)` | `False` |
| `list()` | List | `list("abc")` | `['a','b','c']` |
| `tuple()` | Tuple | `tuple([1,2])` | `(1, 2)` |
| `set()` | Set | `set([1,1,2])` | `{1, 2}` |

```python
# int()
print(int(3.9))       # Output: 3     (truncates, does NOT round)
print(int(3.1))       # Output: 3     (truncates, does NOT round)
print(int("89"))      # Output: 89    (string of digits → int)
print(int(True))      # Output: 1
print(int(False))     # Output: 0

# float()
print(float(5))       # Output: 5.0
print(float("3.14"))  # Output: 3.14

# str()
print(str(89))        # Output: '89'
print(str(3.14))      # Output: '3.14'
print(str(True))      # Output: 'True'

# bool()
print(bool(1))        # Output: True
print(bool(0))        # Output: False
print(bool("hello"))  # Output: True
print(bool(""))       # Output: False
print(bool([1, 2]))   # Output: True
print(bool([]))       # Output: False
print(bool(None))     # Output: False
```

---

### ⚠️ Gotcha — `int()` Truncates, Does NOT Round

```python
print(int(3.9))    # Output: 3  (not 4!)
print(int(-3.9))   # Output: -3 (not -4!)
# int() always cuts off the decimal — it does not round

# To round properly, use round()
print(round(3.9))  # Output: 4
print(round(3.5))  # Output: 4  (banker's rounding)
print(round(2.5))  # Output: 2  (banker's rounding — rounds to even)
```

---

### ⚠️ Gotcha — Truthy and Falsy Values

Every value in Python is either **truthy** or **falsy** when used in a boolean context.

**Falsy values** (evaluate to `False`):
```python
bool(0)        # False — zero int
bool(0.0)      # False — zero float
bool("")       # False — empty string
bool([])       # False — empty list
bool(())       # False — empty tuple
bool({})       # False — empty dict
bool(set())    # False — empty set
bool(None)     # False — None
```

**Truthy values** (everything else evaluates to `True`):
```python
bool(1)        # True
bool(-1)       # True  (any non-zero number)
bool("hello")  # True
bool([0])      # True  (list with one item, even if item is 0)
bool(" ")      # True  (space is not empty)
```

**Why this matters in interviews:**
```python
# These two are equivalent
name = ""
if name:            # checks truthiness
    print("Has name")
else:
    print("Empty")  # Output: Empty

# Same as writing
if bool(name) == True:
    ...
```

---

## 7. `type()` vs `isinstance()`

Both check types but work differently — **commonly asked in interviews**.

```python
x = 89

# type() — returns the exact type
print(type(x))          # Output: <class 'int'>
print(type(x) == int)   # Output: True

# isinstance() — checks if object is instance of a type or its subclass
print(isinstance(x, int))    # Output: True
print(isinstance(x, float))  # Output: False

# isinstance() with multiple types — checks if any match
print(isinstance(x, (int, float)))  # Output: True
```

> **Interview answer:** *"Use `isinstance()` over `type()` because `isinstance()` also returns `True` for subclasses, making it more flexible and Pythonic. `type()` does an exact match only."*

```python
# Example showing the difference
class MyInt(int):
    pass

n = MyInt(5)
print(type(n) == int)       # Output: False (exact match fails — it's MyInt)
print(isinstance(n, int))   # Output: True  (MyInt is a subclass of int)
```

---

## Quick Reference — Number Systems

| Number | Decimal | Binary | Octal | Hex |
|---|---|---|---|---|
| 0 | 0 | 0b0 | 0o0 | 0x0 |
| 8 | 8 | 0b1000 | 0o10 | 0x8 |
| 10 | 10 | 0b1010 | 0o12 | 0xa |
| 16 | 16 | 0b10000 | 0o20 | 0x10 |
| 89 | 89 | 0b1011001 | 0o131 | 0x59 |
| 255 | 255 | 0b11111111 | 0o377 | 0xff |

---

## Interview Short Answers

**Q: What are the numeric types in Python?**
> Python has three numeric types: `int` for whole numbers, `float` for decimal numbers, and `complex` for numbers with real and imaginary parts. Python integers have no size limit unlike C or Java.

**Q: What is the difference between implicit and explicit type conversion?**
> Implicit type conversion is done automatically by Python when mixing types — for example, adding an int and a float gives a float. Explicit type conversion, also called type casting, is done manually using functions like `int()`, `float()`, `str()`, and `bool()`.

**Q: What does `int(3.9)` return?**
> It returns `3`, not `4`. `int()` truncates the decimal part — it does not round. To round a number, use `round()` instead.

**Q: What are falsy values in Python?**
> The falsy values in Python are: `0`, `0.0`, empty string `""`, empty list `[]`, empty tuple `()`, empty dictionary `{}`, empty set `set()`, and `None`. Everything else is truthy.

**Q: What is the difference between `type()` and `isinstance()`?**
> `type()` checks the exact type of an object. `isinstance()` checks if an object is an instance of a type or any of its subclasses. `isinstance()` is preferred because it works correctly with inheritance and is more Pythonic.

**Q: Why does `0.1 + 0.2 != 0.3` in Python?**
> Because floats are stored in binary (base 2) internally, and some decimal fractions like 0.1 cannot be represented exactly in binary. This causes tiny rounding errors. Use `round()` or the `decimal` module when exact precision is needed.
