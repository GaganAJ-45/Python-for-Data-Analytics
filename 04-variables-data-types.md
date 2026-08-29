# Variables and Data Types in Python

## 1. What is a Variable?

A variable is a **name that refers to an object stored in memory**. In Python, you don't store values inside variables — you store references (pointers) to objects.

```text
Variable        Object in Memory
   a  ─────────────→  10
```

```python
a = 10        # 'a' refers to the integer object 10
name = "AJ"   # 'name' refers to the string object "AJ"
```

> **Interview answer:** *"In Python, a variable is not a container — it is a label or reference that points to an object in memory. When you assign a variable, you are making that name point to an object."*

---

## 2. Variable Assignment Types

```python
# Simple assignment
a = 5

# Chained assignment — all refer to the SAME object
b = c = 10
print(b, c)       # Output: 10 10
print(b is c)     # Output: True — same object

# Multiple assignment — one line, multiple variables
x, y, z = 1, 2, 3
print(x, y, z)    # Output: 1 2 3

# Swap two variables — Pythonic way (no temp variable needed)
a, b = 10, 20
a, b = b, a
print(a, b)       # Output: 20 10
```

> **Interview tip:** *"Python's swap `a, b = b, a` works because the right side is fully evaluated first as a tuple `(b, a)`, then unpacked into `a` and `b`."*

---

## 3. Variable Naming Rules

| Rule | ✅ Valid | ❌ Invalid |
|---|---|---|
| Letters, digits, underscores only | `student_1` | `student@1` |
| Cannot start with a digit | `name1` | `1name` |
| No spaces | `first_name` | `first name` |
| Cannot be a keyword | `my_class` | `class` |
| Case-sensitive | `age` and `Age` are different | — |

---

## 4. Naming Conventions (PEP 8)

| Type | Convention | Example |
|---|---|---|
| Variables & functions | `snake_case` | `student_name`, `get_data` |
| Classes | `PascalCase` | `StudentProfile` |
| Constants | `UPPER_CASE` | `MAX_SIZE = 100` |
| Private (convention) | `_single_underscore` | `_helper` |

### Constants in Python
Python has **no true constants** — nothing stops you from changing a value written in `UPPER_CASE`. It is purely a **convention** to signal to other developers: *"don't change this."*

```python
PI = 3.14159          # convention: treat as constant
MAX_CONNECTIONS = 100 # convention: treat as constant

PI = 99  # Python won't stop you — but don't do this
```

---

## 5. Dynamic Typing

Python is **dynamically typed** — the same variable can hold different types at different times. The type is attached to the **object**, not the variable.

```python
x = 10
print(type(x))   # Output: <class 'int'>

x = "hello"
print(type(x))   # Output: <class 'str'>

x = [1, 2, 3]
print(type(x))   # Output: <class 'list'>

x = True
print(type(x))   # Output: <class 'bool'>
```

The variable `x` just keeps pointing to different objects — each with its own type.

---

## 6. Data Types in Python

```
Python Data Types
 ├── Primitive (Single value)
 │    ├── int
 │    ├── float
 │    ├── complex
 │    ├── bool
 │    └── str
 └── Collection (Multiple values)
      ├── list
      ├── tuple
      ├── set
      └── dict
 
Special: NoneType (None)
```

| Type | Example | Mutable? | Ordered? |
|---|---|---|---|
| `int` | `89` | ❌ | — |
| `float` | `3.14` | ❌ | — |
| `complex` | `3+4j` | ❌ | — |
| `bool` | `True`, `False` | ❌ | — |
| `str` | `"hello"` | ❌ | ✅ |
| `list` | `[1, 2, 3]` | ✅ | ✅ |
| `tuple` | `(1, 2, 3)` | ❌ | ✅ |
| `set` | `{1, 2, 3}` | ✅ | ❌ |
| `dict` | `{"a": 1}` | ✅ | ✅ (Python 3.7+) |
| `NoneType` | `None` | ❌ | — |

```python
print(type(89))          # <class 'int'>
print(type(3.14))        # <class 'float'>
print(type(3+4j))        # <class 'complex'>
print(type(True))        # <class 'bool'>
print(type("hello"))     # <class 'str'>
print(type([1, 2]))      # <class 'list'>
print(type((1, 2)))      # <class 'tuple'>
print(type({1, 2}))      # <class 'set'>
print(type({"a": 1}))    # <class 'dict'>
print(type(None))        # <class 'NoneType'>
```

---

## 7. Variables as Object References

This is the most important mental model for Python interviews.

```python
a = 10
```

```text
        ┌───────┐
a ─────→│  10   │  (int object at some memory address)
        └───────┘
```

```python
b = a    # b now refers to the SAME object as a
```

```text
        ┌───────┐
a ─────→│  10   │
        └───────┘
             ↑
b ───────────┘
```

Prove it with `id()` — shows the memory address of the object:

```python
a = 10
b = a

print(id(a))       # e.g. 140712345678912
print(id(b))       # same address — same object
print(a is b)      # True — same object in memory
```

---

## 8. Immutable Objects

An **immutable object cannot be modified** after it is created. When you "change" an immutable variable, Python creates a **new object** and makes the variable point to it.

Types: `int`, `float`, `str`, `tuple`, `bool`, `complex`

```python
a = 10
b = a
```

```text
        ┌───────┐
a ─────→│  10   │
        └───────┘
             ↑
b ───────────┘
```

```python
b = 20    # NOT modifying 10 — creating a new object 20
```

```text
        ┌───────┐
a ─────→│  10   │   (unchanged)
        └───────┘

        ┌───────┐
b ─────→│  20   │   (new object)
        └───────┘
```

```python
print(a)        # Output: 10  (a is unaffected)
print(b)        # Output: 20
print(a is b)   # Output: False (different objects now)
```

---

## 9. Mutable Objects

A **mutable object can be changed** after it is created. The object itself is modified — the variable still points to the same object.

Types: `list`, `dict`, `set`

```python
a = [10, 20, 30]
b = a              # both refer to the SAME list
```

```text
        ┌────────────────┐
a ─────→│ [10, 20, 30]   │
        └────────────────┘
                ↑
b ──────────────┘
```

```python
b[0] = 100    # modifying the SAME object
```

```text
        ┌──────────────────┐
a ─────→│ [100, 20, 30]    │
        └──────────────────┘
                ↑
b ──────────────┘
```

```python
print(a)        # Output: [100, 20, 30]  ← a changed too!
print(b)        # Output: [100, 20, 30]
print(a is b)   # Output: True — still the same object
```

---

## 10. Reassignment vs Modification

This is one of the **most commonly asked** interview questions on Python variables.

### Reassignment — makes variable point to a NEW object

```python
a = [10, 20]
b = a

b = [30, 40]   # b now points to a completely new list
```

```text
a ─────→ [10, 20]   (original — unaffected)
b ─────→ [30, 40]   (new object)
```

```python
print(a)        # Output: [10, 20]  (unchanged)
print(b)        # Output: [30, 40]
print(a is b)   # Output: False
```

### Modification — changes the EXISTING object

```python
a = [10, 20]
b = a

b[0] = 100     # modifies the existing object that both a and b point to
```

```text
a ─────→ [100, 20]
              ↑
b ────────────┘
```

```python
print(a)        # Output: [100, 20]  (a is affected!)
print(b)        # Output: [100, 20]
print(a is b)   # Output: True
```

> **The key question to ask yourself:**
> - `b = something` → **Reassignment** — only `b` is affected
> - `b[i] = something` or `b.method()` → **Modification** — all variables pointing to that object are affected

---

## 11. `==` vs `is`

| Operator | Checks | Question it answers |
|---|---|---|
| `==` | Value equality | "Do they contain the same data?" |
| `is` | Object identity | "Are they literally the same object in memory?" |

```python
# Case 1 — same object
a = [10, 20]
b = a

print(a == b)    # True  — same values
print(a is b)    # True  — same object

# Case 2 — different objects, same values
a = [10, 20]
b = [10, 20]

print(a == b)    # True  — same values
print(a is b)    # False — different objects in memory
print(id(a) == id(b))  # False — different memory addresses
```

```text
Case 2 in memory:

        ┌────────────┐
a ─────→│ [10, 20]   │   (object at address X)
        └────────────┘

        ┌────────────┐
b ─────→│ [10, 20]   │   (object at address Y)
        └────────────┘
```

**Golden rule:** Use `==` for value comparison. Use `is` only to check against `None`.

```python
# Correct use of 'is'
value = None
if value is None:
    print("No value assigned")
```

---

## 12. Global vs Local Variables

```python
x = 10           # global variable — defined outside all functions

def show():
    x = 20       # local variable — only exists inside this function
    print(x)     # Output: 20 (uses local x)

show()
print(x)         # Output: 10 (global x is unchanged)
```

To modify a global variable inside a function, use the `global` keyword:

```python
x = 10

def update():
    global x
    x = 99       # now modifying the global x

update()
print(x)         # Output: 99
```

> **Interview answer:** *"A local variable exists only within the function it is defined in. A global variable is defined at the module level and accessible everywhere. To modify a global variable inside a function, you must declare it with the `global` keyword."*

---

## 13. The `del` Keyword

`del` removes a variable name from the namespace. The object it pointed to may be garbage collected if nothing else references it.

```python
a = [1, 2, 3]
b = a

del a           # removes the name 'a', but the list object still exists
                # because 'b' still refers to it

print(b)        # Output: [1, 2, 3]  — object is still alive

del b           # now nothing refers to the list — Python will garbage collect it

print(b)        # NameError: name 'b' is not defined
```

---

## 14. `None` — Emptying a Variable

Use `None` to represent "no value" or to reset a variable:

```python
result = None         # no value yet

result = calculate()  # assign later when ready

# Check if it has a value
if result is None:
    print("Not calculated yet")
```

---

## Mutable vs Immutable — Full Summary

| Type | Mutable? | What happens on "change"? |
|---|---|---|
| `int` | ❌ | New object created |
| `float` | ❌ | New object created |
| `str` | ❌ | New object created |
| `tuple` | ❌ | New object created |
| `bool` | ❌ | New object created |
| `list` | ✅ | Existing object modified |
| `dict` | ✅ | Existing object modified |
| `set` | ✅ | Existing object modified |

---

## Interview Short Answers

**Q: What is a variable in Python?**
> A variable in Python is not a container — it is a reference or label that points to an object in memory. When you write `a = 10`, you are making the name `a` point to the integer object `10` stored in memory.

**Q: What is the difference between mutable and immutable objects?**
> Immutable objects cannot be changed after creation — types like int, float, str, and tuple. When you reassign them, Python creates a new object. Mutable objects like list, dict, and set can be changed in place — all variables pointing to that object will see the change.

**Q: What is the difference between `==` and `is`?**
> `==` compares values — it checks if two objects contain the same data. `is` compares identity — it checks if two variables point to the exact same object in memory. You should use `==` for value comparison and `is` only for checking against `None`.

**Q: What is the difference between reassignment and modification?**
> Reassignment (`b = new_value`) makes the variable point to a completely new object — the original object is unaffected. Modification (`b[0] = value` or `b.append()`) changes the existing object in place — all variables pointing to that object will see the change.

**Q: What is a global variable? How do you modify it inside a function?**
> A global variable is defined at the module level and accessible throughout the program. To modify it inside a function, you must use the `global` keyword — otherwise Python treats any assignment inside the function as a new local variable.

**Q: Does Python have constants?**
> Python has no built-in constant type. The convention is to write constant names in UPPER_CASE to signal to other developers that the value should not be changed — but Python does not enforce this. Libraries like `typing.Final` can be used to annotate intended constants.
