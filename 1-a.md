## **Python Tokens — Keywords, Identifiers, Literals, Operators, Separators**

### **1. What is a Token?**

A **token** is the smallest meaningful unit of a Python program. Tokens are the building blocks of any Python program — every line of code is broken down into tokens by the interpreter.

There are **5 main categories** of tokens:

```
Tokens
 ├── Keywords
 ├── Identifiers
 ├── Literals
 ├── Operators
 └── Separators
```

---

### **2. Keywords**

- Keywords are **reserved words** in Python that have a special, predefined meaning and cannot be used as identifiers (variable names, function names, etc.).
- There are **35 keywords** in Python (this can change slightly between versions).

You can list all keywords programmatically:

```python
import keyword

kw = keyword.kwlist
print(kw)
print(len(kw))
```

Some of the reserved keywords include:

```
False, None, True, and, or, not, as, assert, async, await,
break, class, continue, def, del, elif, else, except, finally,
for, from, global, if, import, in, is, lambda, nonlocal,
pass, raise, return, try, while, with, yield
```

---

### **3. Identifiers**

Identifiers are the **names used to identify** variables, functions, classes, modules, etc.

**Rules for naming identifiers:**

1. Can start with an underscore (`_`) or an alphabet letter (A–Z, a–z).
2. Cannot start with a number.
3. Cannot contain special characters (`@`, `#`, `%`, `-`, etc.).
4. No spaces allowed between characters of an identifier.
5. Cannot use a reserved keyword as an identifier.
6. Should have a meaningful, full name (not just single random letters, for readability).
7. Can use **camelCase** or **snake_case** naming conventions.

# Python Identifier Tokens

An **identifier** is a name given to a program element such as a **variable, function, class, object, or module**.

> **Identifier = A name used to identify something in a Python program.**

---

## Example

```python
name = "A J"
age = 22

def greet():
    print("Hello")
```

Here:

| Identifier | What it identifies |
|---|---|
| `name` | Variable |
| `age` | Variable |
| `greet` | Function |

---

## Identifier for a Class

```python
class Student:
    pass
```

Here:

```text
Student → Identifier
```

`Student` is the name given to the class.

---

## Rules for Naming Identifiers

### 1. Can contain letters, digits, and underscores

```python
student_name = "A J"
student1 = "Rahul"
```

Valid identifiers:

- `student_name`
- `student1`
- `age`
- `_name`

---

### 2. Cannot start with a digit

❌ Invalid:

```python
1student = "A J"
```

✅ Valid:

```python
student1 = "A J"
```

---

### 3. Cannot contain spaces

❌ Invalid:

```python
student name = "A J"
```

✅ Valid:

```python
student_name = "A J"
```

---

### 4. Cannot use Python keywords

Python keywords already have a special meaning.

❌ Invalid:

```python
if = 10
class = "Student"
```

Because `if` and `class` are Python keywords.

---

### 5. Identifiers are Case-Sensitive

These are **different identifiers**:

```python
age = 20
Age = 30
AGE = 40
```

Python treats:

```text
age
Age
AGE
```

as three different names.

---

## Identifier vs Keyword

Consider:

```python
if age >= 18:
    print(age)
```

Here:

```text
if      → Keyword
age     → Identifier
>=      → Operator
18      → Literal
print   → Identifier
age     → Identifier
```

`if` has a predefined meaning in Python, while `age` is a name used to identify a variable.

> **Identifier = A user-defined name used to identify variables, functions, classes, objects, and other program elements.**

---

### **4. Variables**

- A variable is a **name that acts as a container for a value**.
- Variables are created the moment you assign a value to them.
- Assigning a value to a variable also **allocates memory** for that value.

**Ways to assign values to variables:**

```python
# 1. Simple assignment
a = 5

# 2. Chained assignment - same value to multiple variables
a = b = 5
print(a, b)   # 5 5

# 3. Multiple assignment - different values to multiple variables
a, b = 5, 6
print(a, b)   # 5 6

# 4. Reassigning / swapping
a = 6
b = a
print(a, b)   # 6 6
```

---

### **5. Literals**

A literal is **raw data / a fixed value** given directly in the source code (as opposed to a variable, which refers to a value).

```
Literals
 ├── String Literal
 ├── Numeric Literal ── Decimal, Octal, Hex, Binary
 ├── Boolean Literal
 ├── Special Literal (None)
 └── Literal Collection ── List, Tuple, Set, Dictionary
```

**5.1 String Literals**

Anything inside single quotes `' '` or double quotes `" "` is treated as a string.

```python
name = "AJ"
greeting = 'Hello ' + name    # concatenation -> "Hello AJ"
```

**5.2 Numeric Literals**
Numeric literals represent numbers.

#### Integer Literal

```python
age = 22
count = -10
```

Examples:

- `22`
- `-10`
- `0`

#### Float Literal

```python
price = 99.50
temperature = -2.5
```

Examples:

- `99.50`
- `-2.5`
- `3.14`

#### Complex Literal

```python
z = 3 + 4j
```

Examples:

- `3 + 4j`
- `2j`

---

```python
dec_num = 90        # Decimal
bin_num = 0b1011010  # Binary
oct_num = 0o132      # Octal
hex_num = 0x5A        # Hexadecimal
```

**5.3 Boolean Literals**

```python
is_active = True
is_closed = False
```

**5.4 Special Literal**

```python
value = None   # represents "no value"
```

**5.5 Literal Collections**

```python
my_list = [1, 2, 3]
my_tuple = (1, 2, 3)
my_set = {1, 2, 3}
my_dict = {"key": "value"}
```

---

### **6. Operators**

Operators perform operations on variables and values.

```
Operators
 ├── Arithmetic Operators   (+, -, *, /, %, **, //)
 ├── Assignment Operators   (=, +=, -=, *=, /=, ...)
 ├── Identity Operators      (is, is not)
 ├── Membership Operators    (in, not in)
 ├── Logical Operators       (and, or, not)
 ├── Comparison Operators    (==, !=, >, <, >=, <=)
 └── Bitwise Operators       (&, |, ^, ~, <<, >>)
```

---

### **7. Separators**

Separators are symbols used to separate statements, arguments, or elements — such as commas `,`, colons `:`, semicolons `;`, parentheses `()`, brackets `[]`, and braces `{}`.

---

## Example Containing Different Token Types

Consider the following Python code:

```python
if age >= 18:
    message = "Adult"
    print(message)
```

### Token Identification

| Token | Token Type |
|---|---|
| `if` | Keyword |
| `age` | Identifier |
| `>=` | Operator |
| `18` | Integer Literal |
| `:` | Delimiter |
| `message` | Identifier |
| `=` | Operator |
| `"Adult"` | String Literal |
| `print` | Identifier |
| `(` | Delimiter |
| `message` | Identifier |
| `)` | Delimiter |

### Token Breakdown

```text
if        → Keyword
age       → Identifier
>=        → Operator
18        → Integer Literal
:         → Delimiter
message   → Identifier
=         → Operator
"Adult"   → String Literal
print     → Identifier
(         → Delimiter
message   → Identifier
)         → Delimiter
```

---

## Example with More Token Types

To include **keywords, identifiers, literals, operators, and delimiters** in one example:

```python
def calculate(price, quantity=2):
    total = price * quantity
    if total >= 100:
        return "Discount"
```

### Token Identification

| Token | Token Type |
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

## Main Types of Python Tokens

| Token Type | Examples |
|---|---|
| **Keywords** | `if`, `def`, `return`, `class`, `for` |
| **Identifiers** | `age`, `price`, `total`, `calculate` |
| **Literals** | `10`, `3.14`, `"Hello"`, `True`, `None` |
| **Operators** | `+`, `-`, `*`, `/`, `=`, `>=`, `==` |
| **Delimiters** | `(`, `)`, `[`, `]`, `{`, `}`, `:`, `,` |

> **Token = The smallest meaningful unit of a Python program.**
