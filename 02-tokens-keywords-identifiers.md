# Python Tokens — Keywords, Identifiers, Literals, Operators, Separators

## 1. What is a Token?

A **token** is the **smallest meaningful unit** of a Python program. Before Python executes your code, the interpreter breaks it down into tokens first — this is called **tokenization** and is the very first step of how Python runs your program.

```
Your Code (.py)
      ↓
  Tokenizer          ← breaks code into tokens
      ↓
   Tokens
      ↓
  Parser + Compiler
      ↓
   Bytecode
      ↓
    Output
```

There are **5 main categories** of tokens:

```
Tokens
 ├── Keywords
 ├── Identifiers
 ├── Literals
 ├── Operators
 └── Separators / Delimiters
```

---

## 2. Keywords

Keywords are **reserved words** in Python that have a special, predefined meaning. They **cannot be used** as variable names, function names, or any other identifiers.

- Python currently has **35 keywords** (can vary slightly between versions)
- All keywords are **case-sensitive** — `True` is a keyword, `true` is not

```python
import keyword

print(keyword.kwlist)   # prints all keywords as a list
print(len(keyword.kwlist))  # Output: 35

# Check if a word is a keyword
print(keyword.iskeyword("for"))     # Output: True
print(keyword.iskeyword("name"))    # Output: False
print(keyword.iskeyword("true"))    # Output: False  (case-sensitive)
```

**All 35 keywords:**

```
False    None     True     and      as       assert   async
await    break    class    continue def      del      elif
else     except   finally  for      from     global   if
import   in       is       lambda   nonlocal not      or
pass     raise    return   try      while    with     yield
```

### Keyword Categories

| Category | Keywords |
|---|---|
| Boolean values | `True`, `False`, `None` |
| Logical operators | `and`, `or`, `not` |
| Control flow | `if`, `elif`, `else` |
| Loops | `for`, `while`, `break`, `continue`, `pass` |
| Functions | `def`, `return`, `lambda`, `yield` |
| Classes | `class` |
| Exception handling | `try`, `except`, `finally`, `raise` |
| Import | `import`, `from`, `as` |
| Scope | `global`, `nonlocal`, `del` |
| Identity & membership | `is`, `in` |
| Async programming | `async`, `await` |
| Others | `assert`, `with` |

### ⚠️ Soft Keywords (Python 3.10+)

`match` and `case` are **soft keywords** — they behave like keywords inside a `match` statement but can still be used as variable names elsewhere. This is commonly asked at product company interviews.

```python
match = 10          # valid — 'match' used as variable
case = "hello"      # valid — 'case' used as variable

match command:      # here 'match' acts as a keyword
    case "quit":
        quit()
```

---

## 3. Identifiers

An **identifier** is a **user-defined name** given to a variable, function, class, module, or any other program element.

```python
name = "AJ"        # 'name' is an identifier (variable)
age = 22           # 'age' is an identifier (variable)

def greet():       # 'greet' is an identifier (function)
    print("Hello")

class Student:     # 'Student' is an identifier (class)
    pass
```

| Identifier | What it identifies |
|---|---|
| `name` | Variable |
| `age` | Variable |
| `greet` | Function |
| `Student` | Class |

---

### Rules for Naming Identifiers

**1. Can contain letters, digits, and underscores only**
```python
student_name = "AJ"    # ✅ valid
student1 = "Rahul"     # ✅ valid
_private = 10          # ✅ valid
```

**2. Cannot start with a digit**
```python
1student = "AJ"    # ❌ SyntaxError
student1 = "AJ"    # ✅ valid
```

**3. Cannot contain spaces**
```python
student name = "AJ"    # ❌ SyntaxError
student_name = "AJ"    # ✅ valid
```

**4. Cannot use Python keywords**
```python
if = 10         # ❌ SyntaxError — 'if' is a keyword
class = "test"  # ❌ SyntaxError — 'class' is a keyword
```

**5. Case-sensitive**
```python
age = 20    # different identifier
Age = 30    # different identifier
AGE = 40    # different identifier
# All three are treated as separate variables
```

**6. No length limit — but keep names meaningful**
```python
x = 10                          # ❌ avoid — not meaningful
number_of_students = 10         # ✅ preferred — clear and readable
```

---

### Naming Conventions (PEP 8)

| Type | Convention | Example |
|---|---|---|
| Variables & functions | `snake_case` | `student_name`, `get_data()` |
| Classes | `PascalCase` | `StudentProfile`, `DataLoader` |
| Constants | `UPPER_CASE` | `MAX_SIZE`, `PI` |
| Private (by convention) | `_single_underscore` | `_helper()` |
| Name mangling (OOP) | `__double_underscore` | `__balance` |
| Dunder / Magic | `__double_both_sides__` | `__init__`, `__str__` |

> **PEP 8 recommends `snake_case` for variables and functions — NOT camelCase.** camelCase is a Java/JavaScript convention. In Python, `student_name` is correct, not `studentName`.

---

### Special Identifier Patterns

These are commonly asked in interviews:

**`_name` — Single leading underscore (private by convention)**
```python
class BankAccount:
    def __init__(self):
        self._balance = 1000   # convention: "don't touch this from outside"
```
Not enforced by Python — just a signal to other developers.

**`__name` — Double leading underscore (name mangling)**
```python
class Student:
    def __init__(self):
        self.__marks = 95      # Python renames this to _Student__marks internally
```
Python internally renames it to `_ClassName__attribute` to avoid conflicts in inheritance.

**`__name__` — Dunder / Magic identifiers**
```python
print(__name__)   # Output: __main__ (when running the file directly)
# These are special built-in attributes and methods Python uses internally
# Examples: __init__, __str__, __len__, __repr__
```

---

## 4. Literals

A **literal** is a **fixed, raw value** written directly in the source code. Unlike variables, literals don't change.

```
Literals
 ├── String Literals
 ├── Numeric Literals
 │    ├── Integer (Decimal, Binary, Octal, Hex)
 │    ├── Float
 │    └── Complex
 ├── Boolean Literals
 ├── Special Literal (None)
 └── Collection Literals (List, Tuple, Set, Dict)
```

### 4.1 String Literals

```python
name = "AJ"                        # double quotes
city = 'Bengaluru'                 # single quotes
bio = """I am a Python developer   # triple quotes (multi-line)
from Bengaluru."""
```

### 4.2 Numeric Literals

```python
# Integer literals
age = 22              # Decimal (base 10)
bin_num = 0b1011010   # Binary  (base 2)  — prefix: 0b
oct_num = 0o132       # Octal   (base 8)  — prefix: 0o
hex_num = 0x5A        # Hex     (base 16) — prefix: 0x

# Float literals
price = 99.50
temperature = -2.5
pi = 3.14

# Complex literals
z = 3 + 4j            # real=3, imaginary=4
```

### 4.3 Boolean Literals

```python
is_active = True
is_closed = False
# True and False are keywords AND boolean literals
print(type(True))   # Output: <class 'bool'>
print(int(True))    # Output: 1
print(int(False))   # Output: 0
```

### 4.4 Special Literal — `None`

```python
value = None   # represents "no value" or "empty"
print(type(None))  # Output: <class 'NoneType'>

# Common use: default function return value
def greet():
    print("Hello")
# Functions with no return statement return None by default
```

### 4.5 Collection Literals

```python
my_list  = [1, 2, 3]            # List literal
my_tuple = (1, 2, 3)            # Tuple literal
my_set   = {1, 2, 3}            # Set literal
my_dict  = {"name": "AJ"}       # Dictionary literal
```

---

## 5. Operators

Operators are symbols that perform operations on values and variables. Full coverage is in `06-operators.md`.

```
Operators
 ├── Arithmetic    (+, -, *, /, %, **, //)
 ├── Assignment    (=, +=, -=, *=, /=, ...)
 ├── Comparison    (==, !=, >, <, >=, <=)
 ├── Logical       (and, or, not)
 ├── Identity      (is, is not)
 ├── Membership    (in, not in)
 └── Bitwise       (&, |, ^, ~, <<, >>)
```

---

## 6. Separators / Delimiters

Separators are symbols that **separate or group** elements in code.

| Separator | Name | Used For |
|---|---|---|
| `( )` | Parentheses | Function calls, expressions, tuples |
| `[ ]` | Square brackets | Lists, indexing, slicing |
| `{ }` | Curly braces | Dictionaries, sets |
| `,` | Comma | Separating arguments, elements |
| `:` | Colon | Slicing, dict key-value, block start |
| `;` | Semicolon | Multiple statements on one line |
| `.` | Dot | Attribute/method access |
| `=` | Equals | Assignment |

```python
# Example showing multiple separators
def calculate(price, quantity=2):
    total = price * quantity
    if total >= 100:
        return "Discount"
```

Token breakdown of the above:

| Token | Type |
|---|---|
| `def` | Keyword |
| `calculate` | Identifier |
| `(` | Delimiter |
| `price` | Identifier |
| `,` | Delimiter |
| `quantity` | Identifier |
| `=` | Operator |
| `2` | Integer Literal |
| `)` | Delimiter |
| `:` | Delimiter |
| `total` | Identifier |
| `=` | Operator |
| `price` | Identifier |
| `*` | Operator |
| `quantity` | Identifier |
| `if` | Keyword |
| `total` | Identifier |
| `>=` | Operator |
| `100` | Integer Literal |
| `:` | Delimiter |
| `return` | Keyword |
| `"Discount"` | String Literal |

---

## Quick Reference

| Token Type | Examples |
|---|---|
| **Keywords** | `if`, `def`, `return`, `class`, `for`, `True`, `None` |
| **Identifiers** | `age`, `student_name`, `greet`, `Student` |
| **Literals** | `10`, `3.14`, `"Hello"`, `True`, `None`, `[1,2,3]` |
| **Operators** | `+`, `-`, `*`, `/`, `=`, `>=`, `==`, `and` |
| **Delimiters** | `(`, `)`, `[`, `]`, `{`, `}`, `:`, `,`, `.` |

---

## Interview Short Answers

**Q: What is a token in Python?**
> A token is the smallest meaningful unit of a Python program. The interpreter breaks your source code into tokens before executing it. There are 5 types: keywords, identifiers, literals, operators, and delimiters.

**Q: What is the difference between a keyword and an identifier?**
> Keywords are reserved words with predefined meaning in Python — like `if`, `for`, `def`. You cannot use them as variable names. Identifiers are user-defined names you give to variables, functions, and classes — like `student_name` or `greet`.

**Q: How many keywords does Python have?**
> Python 3 has 35 keywords. You can check them using `import keyword; print(keyword.kwlist)`. You can also check if a specific word is a keyword using `keyword.iskeyword("word")`.

**Q: What is `_name` vs `__name` vs `__name__`?**
> Single underscore `_name` is a convention for private attributes — not enforced by Python, just a signal. Double leading underscore `__name` triggers name mangling — Python renames it to `_ClassName__name` internally to avoid conflicts in inheritance. Double on both sides `__name__` are dunder or magic attributes — special built-in names Python uses internally like `__init__` and `__str__`.

**Q: What is `None` in Python?**
> `None` is a special literal in Python that represents the absence of a value. It is the only instance of `NoneType`. Functions that have no return statement return `None` by default. It is used to represent empty or missing values.
