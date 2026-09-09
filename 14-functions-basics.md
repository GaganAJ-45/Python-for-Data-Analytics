# Functions in Python — Basics

## 1. What is a Function?

A function is a **named, reusable block of code** that performs a specific task. Instead of writing the same code multiple times, you define it once and call it whenever needed.

```
Define once → Call many times
```

**Why use functions?**
- **Reusability** — write once, use anywhere
- **Readability** — break complex code into named steps
- **Maintainability** — fix a bug in one place, fixed everywhere
- **Abstraction** — hide implementation details behind a name

```python
# Without function — repeated code
print("Hello AJ! Welcome.")
print("Hello Rahul! Welcome.")
print("Hello Priya! Welcome.")

# With function — clean and reusable
def greet(name):
    print(f"Hello {name}! Welcome.")

greet("AJ")
greet("Rahul")
greet("Priya")
```

---

## 2. Defining and Calling a Function

**Syntax:**
```python
def function_name(parameters):
    """docstring — optional but recommended"""
    # body
    return value   # optional
```

- `def` — keyword to define a function
- `function_name` — snake_case by PEP 8
- `parameters` — inputs the function accepts (optional)
- `return` — sends a value back to the caller (optional)

```python
# Define
def greet():
    print("Hello! Welcome to Python.")

# Call
greet()   # Output: Hello! Welcome to Python.

# Function is an object — you can inspect it
print(type(greet))   # Output: <class 'function'>
print(greet.__name__)  # Output: greet
```

> **Interview tip:** In Python, functions are **first-class objects** — they can be assigned to variables, passed as arguments, and returned from other functions. This is the foundation of functional programming in Python.

---

## 3. Parameters vs Arguments

These two words are often confused — interviewers ask this directly.

| Term | Definition | Example |
|---|---|---|
| **Parameter** | Variable in the function definition | `def greet(name):` — `name` is parameter |
| **Argument** | Actual value passed when calling | `greet("AJ")` — `"AJ"` is argument |

```python
def add(a, b):       # a and b are PARAMETERS
    return a + b

result = add(10, 20) # 10 and 20 are ARGUMENTS
print(result)        # Output: 30
```

---

## 4. Types of Arguments

### 4.1 Positional Arguments
Matched by **position** — order matters.

```python
def describe(name, age, city):
    print(f"{name} is {age} years old from {city}")

describe("AJ", 22, "Bengaluru")   # correct order
# Output: AJ is 22 years old from Bengaluru

describe(22, "AJ", "Bengaluru")   # wrong order — age and name swapped
# Output: 22 is AJ years old from Bengaluru
```

### 4.2 Keyword Arguments
Matched by **name** — order doesn't matter.

```python
describe(age=22, city="Bengaluru", name="AJ")
# Output: AJ is 22 years old from Bengaluru

# Mix — positional first, keyword after
describe("AJ", city="Bengaluru", age=22)
# Output: AJ is 22 years old from Bengaluru
```

> ⚠️ Positional arguments must always come **before** keyword arguments:
> ```python
> describe(name="AJ", 22, "Bengaluru")  # ❌ SyntaxError
> ```

### 4.3 Default Arguments
Parameter has a **default value** — used when argument is not provided.

```python
def greet(name, message="Welcome to Python!"):
    print(f"Hello {name}! {message}")

greet("AJ")                          # uses default
# Output: Hello AJ! Welcome to Python!

greet("AJ", "Good to see you!")      # overrides default
# Output: Hello AJ! Good to see you!
```

> ⚠️ **Interview gotcha — Mutable default arguments:**
> ```python
> # WRONG — list is created ONCE and shared across all calls
> def add_item(item, lst=[]):
>     lst.append(item)
>     return lst
>
> print(add_item("a"))   # Output: ['a']
> print(add_item("b"))   # Output: ['a', 'b']  ← 'a' still there!
> print(add_item("c"))   # Output: ['a', 'b', 'c']
>
> # CORRECT — use None as default, create new list inside
> def add_item(item, lst=None):
>     if lst is None:
>         lst = []
>     lst.append(item)
>     return lst
>
> print(add_item("a"))   # Output: ['a']
> print(add_item("b"))   # Output: ['b']  ← fresh list each time
> ```
> This is one of the most asked Python gotchas in interviews.

---

## 5. Return Statement

`return` sends a value back to the caller and **exits the function immediately**.

```python
def add(a, b):
    return a + b

result = add(10, 20)
print(result)   # Output: 30
```

### Function with no return statement
Returns `None` by default.

```python
def greet(name):
    print(f"Hello {name}!")

result = greet("AJ")
print(result)   # Output: None
```

### Returning multiple values
Python returns them as a **tuple**.

```python
def get_student():
    name = "AJ"
    age  = 22
    city = "Bengaluru"
    return name, age, city   # returns tuple (name, age, city)

# Unpack directly
name, age, city = get_student()
print(name, age, city)   # Output: AJ 22 Bengaluru

# Or keep as tuple
info = get_student()
print(info)        # Output: ('AJ', 22, 'Bengaluru')
print(type(info))  # Output: <class 'tuple'>
```

### Early return — exit function before end
```python
def divide(a, b):
    if b == 0:
        return "Cannot divide by zero"   # exits here
    return a / b

print(divide(10, 2))   # Output: 5.0
print(divide(10, 0))   # Output: Cannot divide by zero
```

---

## 6. Scope — Local and Global Variables

**Scope** defines where a variable can be accessed.

```
LEGB Rule — Python looks up variables in this order:
L → Local    (inside the current function)
E → Enclosing (in outer function — for nested functions)
G → Global   (at module level)
B → Built-in (Python's built-in names like len, print)
```

### Local Scope
Variable defined inside a function — only accessible inside that function.

```python
def show():
    x = 10        # local variable
    print(x)      # Output: 10

show()
print(x)          # ❌ NameError — x doesn't exist outside
```

### Global Scope
Variable defined outside all functions — accessible everywhere.

```python
x = 10            # global variable

def show():
    print(x)      # ✅ can READ global variable

show()            # Output: 10
print(x)          # Output: 10
```

### Local vs Global — same name
```python
x = 10            # global x

def show():
    x = 20        # local x — completely separate from global x
    print(x)      # Output: 20  (uses local)

show()
print(x)          # Output: 10  (global unchanged)
```

### `global` keyword — modify global inside function
```python
count = 0         # global

def increment():
    global count  # declare intent to modify global
    count += 1

increment()
increment()
print(count)      # Output: 2
```

> ⚠️ **Interview tip:** Avoid `global` as much as possible — it makes code hard to test and debug. Prefer returning values instead of modifying globals.

---

## 7. `nonlocal` keyword

Used in **nested functions** to modify a variable in the enclosing (outer) function's scope.

```python
def outer():
    count = 0           # enclosing scope

    def inner():
        nonlocal count  # refers to outer's count
        count += 1

    inner()
    inner()
    print(count)        # Output: 2

outer()
```

---

## 8. Docstrings

A docstring is a string literal right after the `def` line — documents what the function does.

```python
def add(a, b):
    """
    Add two numbers and return the result.

    Args:
        a (int): first number
        b (int): second number

    Returns:
        int: sum of a and b
    """
    return a + b

# Access the docstring
print(add.__doc__)
help(add)
```

> **Interview tip:** Always write docstrings in production code. It shows professional coding habits. Interviewers notice this.

---

## 9. Functions are First-Class Objects

In Python, functions are objects — they can be:
- Assigned to variables
- Passed as arguments
- Returned from other functions
- Stored in data structures

```python
def greet(name):
    return f"Hello {name}!"

# Assign to variable
say_hello = greet
print(say_hello("AJ"))   # Output: Hello AJ!

# Store in a list
operations = [greet, str.upper, str.lower]
print(operations[0]("AJ"))   # Output: Hello AJ!

# Pass as argument
def apply(func, value):
    return func(value)

print(apply(greet, "Rahul"))   # Output: Hello Rahul!
```

---

## 10. Pure Functions vs Impure Functions

### Pure Function
- Always returns the same output for the same input
- No side effects — doesn't modify anything outside itself

```python
# Pure — same input always gives same output
def add(a, b):
    return a + b

print(add(2, 3))   # always 5
print(add(2, 3))   # always 5
```

### Impure Function
- May return different output for same input
- Has side effects — modifies external state

```python
total = 0

# Impure — modifies external variable
def add_to_total(n):
    global total
    total += n
    return total

print(add_to_total(5))   # 5
print(add_to_total(5))   # 10 — different output same input!
```

> **Interview tip:** Prefer pure functions — easier to test, debug, and reason about. Functional programming is built on pure functions.

---

## 11. Common Built-in Functions You Should Know

```python
# Type and conversion
print(type(x))          # type of object
print(isinstance(x, int))  # type check

# Iterables
print(len([1,2,3]))     # length
print(range(1, 10, 2))  # range object
print(list(range(5)))   # [0,1,2,3,4]
print(enumerate(lst))   # index + value
print(zip(l1, l2))      # pair elements

# Math
print(abs(-5))          # 5
print(round(3.7))       # 4
print(min(1,2,3))       # 1
print(max(1,2,3))       # 3
print(sum([1,2,3]))     # 6
print(pow(2, 8))        # 256

# Sorting
print(sorted([3,1,2]))          # [1,2,3]
print(sorted([3,1,2], reverse=True))  # [3,2,1]

# Input/Output
name = input("Enter: ")
print("Hello", name, sep=", ", end="!\n")
```

---

## 12. Interview Patterns Using Functions

### Utility / Helper Function Pattern
```python
def is_prime(n):
    """Check if n is prime — reusable helper"""
    if n < 2:
        return False
    for i in range(2, int(n**0.5) + 1):
        if n % i == 0:
            return False
    return True

# Use in multiple places
primes = [n for n in range(2, 50) if is_prime(n)]
print(primes)
```

### Validate + Process Pattern
```python
def get_positive_number(prompt):
    """Keep asking until valid positive number entered"""
    while True:
        try:
            num = int(input(prompt))
            if num > 0:
                return num
            print("Must be positive. Try again.")
        except ValueError:
            print("Must be a number. Try again.")

num = get_positive_number("Enter a positive number: ")
print(f"You entered: {num}")
```

### Guard Clause Pattern — early return
```python
# Without guard clauses — deeply nested
def process(data):
    if data is not None:
        if len(data) > 0:
            if isinstance(data, list):
                return sum(data)

# With guard clauses — flat and readable
def process(data):
    if data is None:
        return 0
    if len(data) == 0:
        return 0
    if not isinstance(data, list):
        return 0
    return sum(data)
```

---

## Quick Reference

```python
# DEFINE
def function_name(params):
    """docstring"""
    body
    return value

# CALL
result = function_name(args)

# ARGUMENT TYPES
func(10, 20)                  # positional
func(a=10, b=20)              # keyword
func(10, b=20)                # mixed — positional first

# DEFAULT PARAMS
def func(a, b=10):            # b has default
    pass

# RETURN
return value                  # single value
return a, b, c                # multiple — returns tuple
return                        # returns None
# no return → returns None

# SCOPE
x = 10                        # global
def f():
    x = 20                    # local — shadows global
    global x; x = 20          # modify global
    nonlocal x                # modify enclosing scope

# FIRST CLASS
f2 = f1                       # assign
apply(f1, arg)                # pass as argument
return f1                     # return from function

# DOCSTRING
def func():
    """What this does."""
    pass
func.__doc__                  # access docstring
```

---

## Interview Short Answers

**Q: What is a function in Python?**
> A function is a named, reusable block of code that performs a specific task. It is defined using the `def` keyword. Functions help avoid code repetition, improve readability, and make programs easier to maintain. In Python, functions are first-class objects — they can be assigned to variables, passed as arguments, and returned from other functions.

**Q: What is the difference between a parameter and an argument?**
> A parameter is the variable defined in the function signature — it is a placeholder. An argument is the actual value passed when the function is called. For example, in `def greet(name)`, `name` is a parameter. In `greet("AJ")`, `"AJ"` is the argument.

**Q: What is the difference between positional and keyword arguments?**
> Positional arguments are matched by their position — order matters. Keyword arguments are matched by name — order doesn't matter. You can mix them but positional arguments must always come before keyword arguments. Keyword arguments make function calls more readable and less error-prone.

**Q: What is the mutable default argument gotcha?**
> When a mutable object like a list or dict is used as a default parameter value, it is created only once when the function is defined — not each time the function is called. This means all calls share the same object, which causes unexpected behavior. The fix is to use `None` as the default and create a new object inside the function: `def func(lst=None): if lst is None: lst = []`.

**Q: What does a function return if there is no return statement?**
> It returns `None`. In Python, every function returns a value. If no `return` statement is present, or if `return` is used without a value, the function implicitly returns `None`.

**Q: What is the LEGB rule?**
> LEGB stands for Local, Enclosing, Global, Built-in — the order in which Python looks up variable names. First it checks the local scope (current function), then enclosing scope (outer function for nested functions), then global scope (module level), then built-in scope (Python's built-in names like `len` and `print`).

**Q: What is the difference between `global` and `nonlocal`?**
> `global` is used inside a function to declare that a variable refers to the module-level global variable, allowing you to modify it. `nonlocal` is used inside a nested function to declare that a variable refers to the variable in the nearest enclosing function's scope, allowing you to modify it. Without these keywords, assignment inside a function always creates a new local variable.

**Q: What is a pure function?**
> A pure function always returns the same output for the same input and has no side effects — it does not modify any external state. Pure functions are easier to test, debug, and reason about. Examples are mathematical functions like `add(a, b): return a + b`. An impure function modifies global state or depends on external variables, making its behavior unpredictable.
