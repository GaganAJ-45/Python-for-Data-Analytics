# Functions in Python — Advanced
---

## 1. `*args` — Variable Positional Arguments

`*args` allows a function to accept **any number of positional arguments**. They are collected into a **tuple** inside the function.

```python
def add(*args):
    print(args)         # tuple
    print(type(args))   # <class 'tuple'>
    return sum(args)

print(add(1, 2))           # Output: 3
print(add(1, 2, 3, 4, 5)) # Output: 15
print(add())               # Output: 0
```

```python
# Mix with regular parameters — regular params come first
def greet(greeting, *names):
    for name in names:
        print(f"{greeting}, {name}!")

greet("Hello", "AJ", "Rahul", "Priya")
# Hello, AJ!
# Hello, Rahul!
# Hello, Priya!
```

```python
# Unpack a list into positional args using *
def add(a, b, c):
    return a + b + c

numbers = [1, 2, 3]
print(add(*numbers))   # Output: 6
# *numbers unpacks [1,2,3] into separate args
```

---

## 2. `**kwargs` — Variable Keyword Arguments

`**kwargs` allows a function to accept **any number of keyword arguments**. They are collected into a **dictionary** inside the function.

```python
def display(**kwargs):
    print(kwargs)         # dict
    print(type(kwargs))   # <class 'dict'>
    for key, value in kwargs.items():
        print(f"{key}: {value}")

display(name="AJ", age=22, city="Bengaluru")
# {'name': 'AJ', 'age': 22, 'city': 'Bengaluru'}
# name: AJ
# age: 22
# city: Bengaluru
```

```python
# Unpack a dict into keyword args using **
def student_info(name, age, city):
    print(f"{name} is {age} from {city}")

data = {"name": "AJ", "age": 22, "city": "Bengaluru"}
student_info(**data)   # Output: AJ is 22 from Bengaluru
```

---

## 3. Combining All Parameter Types

The order must always be:
```
def func(regular, *args, keyword_only, **kwargs)
```

```python
def show(a, b, *args, sep=", ", **kwargs):
    print(f"a={a}, b={b}")
    print(f"extra args: {args}")
    print(f"sep: {sep}")
    print(f"kwargs: {kwargs}")

show(1, 2, 3, 4, 5, sep="-", name="AJ", city="Bengaluru")
# a=1, b=2
# extra args: (3, 4, 5)
# sep: -
# kwargs: {'name': 'AJ', 'city': 'Bengaluru'}
```

**Order rule — must follow this sequence:**
```
1. Regular positional parameters    →  def f(a, b)
2. *args                            →  def f(a, *args)
3. Keyword-only parameters          →  def f(a, *args, key=val)
4. **kwargs                         →  def f(a, *args, **kwargs)
```

> **Interview tip:** `*args` gives a tuple, `**kwargs` gives a dict. The names `args` and `kwargs` are just convention — `*numbers` and `**options` work too. What matters is the `*` and `**`.

---

## 4. Lambda Functions

A lambda is a **small, anonymous, one-line function** — defined with the `lambda` keyword instead of `def`.

```python
# Syntax
lambda parameters: expression

# Regular function
def square(x):
    return x ** 2

# Lambda equivalent
square = lambda x: x ** 2
print(square(5))   # Output: 25
```

```python
# Multiple parameters
add  = lambda a, b: a + b
print(add(3, 4))   # Output: 7

# With condition
even_odd = lambda n: "even" if n % 2 == 0 else "odd"
print(even_odd(5))   # Output: odd
```

**Where lambdas shine — as arguments to other functions:**
```python
numbers = [5, 2, 8, 1, 9, 3]

# Sort using lambda
print(sorted(numbers))                          # [1, 2, 3, 5, 8, 9]
print(sorted(numbers, key=lambda x: -x))       # [9, 8, 5, 3, 2, 1]

# Sort list of tuples by second element
pairs = [(1, 3), (2, 1), (3, 2)]
print(sorted(pairs, key=lambda x: x[1]))       # [(2,1), (3,2), (1,3)]

# Sort list of dicts by field
students = [{"name": "AJ", "marks": 85}, {"name": "Rahul", "marks": 92}]
print(sorted(students, key=lambda s: s["marks"], reverse=True))
```

> **When NOT to use lambda:**
> - When the logic is complex — use `def` instead
> - When you need a docstring
> - When you need to reuse it in many places
>
> Lambda is best for short, throwaway functions passed as arguments.

---

## 5. `map()` — Apply Function to Every Element

`map(function, iterable)` applies a function to **every element** of an iterable and returns a map object (lazy).

```python
numbers = [1, 2, 3, 4, 5]

# Square every number
squared = list(map(lambda x: x**2, numbers))
print(squared)   # Output: [1, 4, 9, 16, 25]

# Convert strings to integers
str_nums = ["1", "2", "3", "4"]
int_nums = list(map(int, str_nums))
print(int_nums)  # Output: [1, 2, 3, 4]

# With a named function
def celsius_to_fahrenheit(c):
    return (c * 9/5) + 32

temps_c = [0, 20, 37, 100]
temps_f = list(map(celsius_to_fahrenheit, temps_c))
print(temps_f)   # Output: [32.0, 68.0, 98.6, 212.0]

# map with multiple iterables
a = [1, 2, 3]
b = [10, 20, 30]
result = list(map(lambda x, y: x + y, a, b))
print(result)    # Output: [11, 22, 33]
```

**`map()` vs list comprehension:**
```python
# map
squared = list(map(lambda x: x**2, numbers))

# comprehension — more readable, preferred in Python
squared = [x**2 for x in numbers]
```

> **Interview tip:** Both `map()` and list comprehension do the same thing. In Python, list comprehension is generally preferred for readability. Use `map()` when passing an already-defined function like `int`, `str`, `float`.

---

## 6. `filter()` — Keep Elements That Pass a Test

`filter(function, iterable)` keeps only elements where the function returns `True`.

```python
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

# Keep only even numbers
evens = list(filter(lambda x: x % 2 == 0, numbers))
print(evens)   # Output: [2, 4, 6, 8, 10]

# Keep only positive numbers
mixed = [-3, -1, 0, 2, 5, -8, 4]
positives = list(filter(lambda x: x > 0, mixed))
print(positives)   # Output: [2, 5, 4]

# Filter strings longer than 4 characters
words = ["cat", "elephant", "dog", "python", "ant"]
long_words = list(filter(lambda w: len(w) > 4, words))
print(long_words)   # Output: ['elephant', 'python']

# filter with None — removes falsy values
mixed = [0, 1, "", "hello", None, [], [1,2], False, True]
truthy = list(filter(None, mixed))
print(truthy)   # Output: [1, 'hello', [1, 2], True]
```

**`filter()` vs list comprehension:**
```python
# filter
evens = list(filter(lambda x: x % 2 == 0, numbers))

# comprehension — cleaner
evens = [x for x in numbers if x % 2 == 0]
```

---

## 7. `reduce()` — Reduce to a Single Value

`reduce(function, iterable)` applies a function cumulatively to reduce an iterable to a single value. From `functools` module.

```python
from functools import reduce

numbers = [1, 2, 3, 4, 5]

# Sum all numbers
total = reduce(lambda acc, x: acc + x, numbers)
print(total)   # Output: 15
# Step: 1+2=3 → 3+3=6 → 6+4=10 → 10+5=15

# Product of all numbers
product = reduce(lambda acc, x: acc * x, numbers)
print(product)   # Output: 120
# Step: 1*2=2 → 2*3=6 → 6*4=24 → 24*5=120

# Find maximum
maximum = reduce(lambda a, b: a if a > b else b, numbers)
print(maximum)   # Output: 5

# With initial value
total = reduce(lambda acc, x: acc + x, numbers, 100)
print(total)   # Output: 115  (starts from 100)
```

**`reduce()` vs built-ins:**
```python
# reduce is rarely needed — built-ins are cleaner
reduce(lambda a, b: a + b, lst)   →   sum(lst)
reduce(lambda a, b: a * b, lst)   →   math.prod(lst)  # Python 3.8+
reduce(lambda a, b: max(a,b), lst) →  max(lst)
```

> **Interview tip:** Know `reduce()` conceptually but prefer built-ins like `sum()`, `max()`, `min()` in real code. Interviewers ask about it to test functional programming knowledge.

---

## 8. `map`, `filter`, `reduce` — Side by Side

```python
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

# map    — transform each element
doubled = list(map(lambda x: x * 2, numbers))
# [2, 4, 6, 8, 10, 12, 14, 16, 18, 20]

# filter — keep elements that pass test
evens   = list(filter(lambda x: x % 2 == 0, numbers))
# [2, 4, 6, 8, 10]

# reduce — collapse to one value
total   = reduce(lambda a, b: a + b, numbers)
# 55

# Chain them — filter evens, square them, sum the result
from functools import reduce
result = reduce(
    lambda a, b: a + b,
    map(lambda x: x**2,
        filter(lambda x: x % 2 == 0, numbers))
)
print(result)   # Output: 220  (4+16+36+64+100)

# Same thing with comprehension — much cleaner
result = sum(x**2 for x in numbers if x % 2 == 0)
print(result)   # Output: 220
```

---

## 9. Nested Functions

A function defined **inside another function**. The inner function has access to the outer function's variables.

```python
def outer():
    message = "Hello from outer"

    def inner():
        print(message)    # can access outer's variable

    inner()               # call inner inside outer

outer()   # Output: Hello from outer
```

```python
# Practical use — helper function that shouldn't be exposed
def process_data(data):
    def clean(item):
        return item.strip().lower()

    return [clean(item) for item in data]

result = process_data(["  AJ  ", " PYTHON ", "  CODE "])
print(result)   # Output: ['aj', 'python', 'code']
```

---

## 10. Closures

A closure is a nested function that **remembers the variables from its enclosing scope** even after the outer function has finished executing.

```python
def make_multiplier(factor):
    def multiply(number):
        return number * factor    # 'factor' remembered from outer scope
    return multiply               # return the inner function

double = make_multiplier(2)
triple = make_multiplier(3)

print(double(5))    # Output: 10  (5 * 2)
print(triple(5))    # Output: 15  (5 * 3)
print(double(10))   # Output: 20

# factor=2 is remembered inside double
# factor=3 is remembered inside triple
```

```python
# Closure for counter
def make_counter():
    count = 0

    def counter():
        nonlocal count
        count += 1
        return count

    return counter

c1 = make_counter()
c2 = make_counter()

print(c1())   # Output: 1
print(c1())   # Output: 2
print(c1())   # Output: 3
print(c2())   # Output: 1  ← independent counter
```

**Three conditions for a closure:**
1. There must be a nested function
2. The nested function must refer to a variable in the enclosing scope
3. The enclosing function must return the nested function

```python
# Check closure variables
print(double.__closure__)           # shows closure cells
print(double.__closure__[0].cell_contents)   # Output: 2
```

> **Interview answer:** *"A closure is a function that retains access to variables from its enclosing scope even after that scope has finished executing. It is created when an inner function references a variable from the outer function and the outer function returns the inner function."*

---

## 11. Decorators

A decorator is a function that **wraps another function** to extend or modify its behavior — without changing the original function's code.

```
Original function → Decorator wraps it → Enhanced function
```

### Understanding Step by Step

```python
# Step 1 — a simple decorator
def my_decorator(func):
    def wrapper():
        print("Before the function runs")
        func()
        print("After the function runs")
    return wrapper

def greet():
    print("Hello!")

# Step 2 — apply manually
greet = my_decorator(greet)
greet()
# Before the function runs
# Hello!
# After the function runs
```

### Using `@` Syntax — Syntactic Sugar

```python
def my_decorator(func):
    def wrapper():
        print("Before")
        func()
        print("After")
    return wrapper

@my_decorator          # same as: greet = my_decorator(greet)
def greet():
    print("Hello!")

greet()
# Before
# Hello!
# After
```

### Decorator with Arguments — use `*args, **kwargs`

```python
def my_decorator(func):
    def wrapper(*args, **kwargs):    # pass through all arguments
        print(f"Calling {func.__name__}")
        result = func(*args, **kwargs)
        print(f"Done")
        return result
    return wrapper

@my_decorator
def add(a, b):
    return a + b

print(add(3, 4))
# Calling add
# Done
# 7
```

### Real-World Decorator Examples

**Timer decorator — measure execution time:**
```python
import time

def timer(func):
    def wrapper(*args, **kwargs):
        start  = time.time()
        result = func(*args, **kwargs)
        end    = time.time()
        print(f"{func.__name__} took {end - start:.4f} seconds")
        return result
    return wrapper

@timer
def slow_function():
    time.sleep(1)
    return "Done"

slow_function()   # Output: slow_function took 1.0012 seconds
```

**Logger decorator:**
```python
def logger(func):
    def wrapper(*args, **kwargs):
        print(f"Calling {func.__name__} with args={args} kwargs={kwargs}")
        result = func(*args, **kwargs)
        print(f"{func.__name__} returned {result}")
        return result
    return wrapper

@logger
def multiply(a, b):
    return a * b

multiply(3, 4)
# Calling multiply with args=(3, 4) kwargs={}
# multiply returned 12
```

**`functools.wraps` — preserve function metadata:**
```python
from functools import wraps

def my_decorator(func):
    @wraps(func)           # preserves __name__, __doc__ of original
    def wrapper(*args, **kwargs):
        return func(*args, **kwargs)
    return wrapper

@my_decorator
def greet():
    """Greets the user"""
    print("Hello!")

print(greet.__name__)   # Output: greet  (not 'wrapper')
print(greet.__doc__)    # Output: Greets the user
```

### Stacking Multiple Decorators
```python
def bold(func):
    def wrapper():
        return "<b>" + func() + "</b>"
    return wrapper

def italic(func):
    def wrapper():
        return "<i>" + func() + "</i>"
    return wrapper

@bold
@italic           # applied bottom-up: italic first, then bold
def text():
    return "Hello"

print(text())   # Output: <b><i>Hello</i></b>
```

> **Interview tip:** Decorators are used everywhere in Python frameworks — `@app.route` in Flask, `@property`, `@staticmethod`, `@classmethod` in OOP, `@login_required` in Django. Understanding decorators shows you understand Python deeply.

---

## 12. Higher-Order Functions

A function that **takes another function as argument** or **returns a function**.

```python
# Takes a function as argument
def apply_twice(func, value):
    return func(func(value))

def double(x):
    return x * 2

print(apply_twice(double, 3))   # Output: 12  (3→6→12)

# Returns a function
def make_adder(n):
    return lambda x: x + n

add5  = make_adder(5)
add10 = make_adder(10)

print(add5(3))    # Output: 8
print(add10(3))   # Output: 13
```

---

## 13. `functools` Module — Essential Tools

```python
from functools import reduce, wraps, lru_cache, partial

# lru_cache — memoization (cache function results)
@lru_cache(maxsize=None)
def fibonacci(n):
    if n < 2:
        return n
    return fibonacci(n-1) + fibonacci(n-2)

print(fibonacci(50))   # instant — cached results reused
# Without cache this would be extremely slow

# partial — fix some arguments of a function
from functools import partial

def power(base, exponent):
    return base ** exponent

square = partial(power, exponent=2)
cube   = partial(power, exponent=3)

print(square(4))   # Output: 16
print(cube(3))     # Output: 27
```

> **Interview tip:** `lru_cache` (Least Recently Used cache) is the Python built-in way to do memoization. It caches the return value of a function based on its arguments. Asking to optimize a recursive solution is very common — mentioning `lru_cache` shows practical Python knowledge.

---

## Quick Reference

```python
# *args — variable positional → tuple
def func(*args):
    for arg in args: ...

# **kwargs — variable keyword → dict
def func(**kwargs):
    for k, v in kwargs.items(): ...

# Combined order
def func(a, b, *args, key=val, **kwargs): ...

# Unpack
func(*list)       # unpack list into positional args
func(**dict)      # unpack dict into keyword args

# LAMBDA
f = lambda x: x**2
f = lambda x, y: x + y
f = lambda x: "even" if x%2==0 else "odd"

# MAP — transform each element
list(map(func, iterable))
list(map(lambda x: x**2, numbers))

# FILTER — keep elements where func returns True
list(filter(func, iterable))
list(filter(lambda x: x > 0, numbers))
list(filter(None, lst))        # remove falsy values

# REDUCE — collapse to one value
from functools import reduce
reduce(lambda acc, x: acc + x, lst)
reduce(lambda acc, x: acc + x, lst, initial)

# CLOSURE
def outer():
    x = 10
    def inner():
        return x    # remembers x
    return inner

# DECORATOR
def decorator(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        # before
        result = func(*args, **kwargs)
        # after
        return result
    return wrapper

@decorator
def my_func(): ...

# LRU CACHE
from functools import lru_cache
@lru_cache(maxsize=None)
def expensive_func(n): ...

# PARTIAL
from functools import partial
new_func = partial(func, fixed_arg=value)
```

---

## Interview Short Answers

**Q: What is the difference between `*args` and `**kwargs`?**
> `*args` collects extra positional arguments into a tuple — used when you don't know how many positional arguments will be passed. `**kwargs` collects extra keyword arguments into a dictionary — used when you don't know how many named arguments will be passed. They can be combined but must follow the order: regular params, then `*args`, then keyword-only params, then `**kwargs`.

**Q: What is a lambda function? When should you use it?**
> A lambda is a small anonymous function defined in one line using the `lambda` keyword: `lambda params: expression`. It can only contain a single expression — no statements, loops, or multiple lines. Use lambda for short throwaway functions passed as arguments to `sorted()`, `map()`, or `filter()`. For anything complex, use a regular `def` function instead.

**Q: What is the difference between `map()`, `filter()`, and `reduce()`?**
> `map()` applies a function to every element and returns the transformed elements. `filter()` applies a function and keeps only elements where it returns True. `reduce()` applies a function cumulatively to reduce the entire iterable to a single value. In modern Python, list comprehensions are preferred over `map()` and `filter()` for readability. `reduce()` requires importing from `functools`.

**Q: What is a closure in Python?**
> A closure is a nested function that remembers variables from its enclosing scope even after the outer function has finished executing. Three things are needed: a nested function, the nested function must use a variable from the outer scope, and the outer function must return the inner function. Closures are used to create function factories and maintain state without using classes.

**Q: What is a decorator in Python?**
> A decorator is a function that wraps another function to add behavior before or after it runs — without modifying the original function. Applied using the `@` syntax, which is shorthand for `func = decorator(func)`. Decorators are used for logging, timing, authentication, and caching. Always use `@functools.wraps` inside a decorator to preserve the original function's metadata.

**Q: What is `lru_cache` and when do you use it?**
> `lru_cache` from `functools` is a decorator that caches the return value of a function based on its arguments. When the same arguments are passed again, it returns the cached result instead of recomputing. LRU stands for Least Recently Used — it evicts the least recently used cached results when the cache is full. It is used to optimize recursive functions like Fibonacci, where the same subproblems are computed repeatedly. With `@lru_cache`, Fibonacci goes from O(2ⁿ) to O(n).

**Q: What is the difference between a closure and a decorator?**
> Both use nested functions and closures — but they serve different purposes. A closure is used to create functions that remember state from their enclosing scope, like a function factory (`make_multiplier(2)`). A decorator specifically wraps an existing function to modify or extend its behavior, and is applied using the `@` syntax. Decorators are built on top of the closure concept.

**Q: What is `functools.partial`?**
> `partial` creates a new function with some arguments of an existing function pre-filled. For example, `square = partial(power, exponent=2)` creates a new function where `exponent` is always 2. It is useful when you want to specialize a general function for a specific use case without rewriting it.
