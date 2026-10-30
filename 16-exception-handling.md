# Exception Handling in Python
> Foundation Notes — Interview Ready | DSA Focused

---

## 1. What is an Exception?

An exception is an **error that occurs during program execution** — it disrupts the normal flow. Without handling, exceptions crash the program.

```python
# This crashes the program
print(10 / 0)
# ZeroDivisionError: division by zero

print("This line never runs")   # never reached
```

**Errors vs Exceptions:**

| | Error | Exception |
|---|---|---|
| Type | Serious — program cannot continue | Recoverable — can be handled |
| Examples | `SyntaxError`, `IndentationError` | `ValueError`, `ZeroDivisionError` |
| Caught by try/except? | ❌ No (caught before running) | ✅ Yes |

---

## 2. Common Built-in Exceptions

| Exception | When it occurs |
|---|---|
| `ZeroDivisionError` | Dividing by zero |
| `ValueError` | Wrong value — `int("hello")` |
| `TypeError` | Wrong type — `"5" + 5` |
| `IndexError` | List index out of range |
| `KeyError` | Dictionary key not found |
| `AttributeError` | Attribute doesn't exist on object |
| `NameError` | Variable not defined |
| `FileNotFoundError` | File doesn't exist |
| `ImportError` | Module not found |
| `RecursionError` | Max recursion depth exceeded |
| `StopIteration` | Iterator exhausted |
| `AssertionError` | `assert` statement failed |

---

## 3. `try-except` — Basic Handling

```python
try:
    result = 10 / 0           # code that might fail
except ZeroDivisionError:
    print("Cannot divide by zero!")   # runs only on that error

print("Program continues...")
# Output:
# Cannot divide by zero!
# Program continues...
```

**Without try-except → program crashes:**
```python
result = 10 / 0              # ZeroDivisionError — crash!
print("This never runs")
```

**With try-except → program recovers:**
```python
try:
    result = 10 / 0
except ZeroDivisionError:
    print("Handled!")
print("This runs!")          # ✅ continues normally
```

---

## 4. Catching Multiple Exceptions

### Multiple `except` blocks — handle each differently
```python
def safe_divide(a, b):
    try:
        result = a / b
        print(f"Result: {result}")
    except ZeroDivisionError:
        print("Error: Cannot divide by zero")
    except TypeError:
        print("Error: Both values must be numbers")

safe_divide(10, 2)       # Output: Result: 5.0
safe_divide(10, 0)       # Output: Error: Cannot divide by zero
safe_divide(10, "two")   # Output: Error: Both values must be numbers
```

### Catch multiple in one `except` — tuple
```python
try:
    value = int(input("Enter a number: "))
    result = 10 / value
except (ValueError, ZeroDivisionError) as e:
    print(f"Error: {e}")
```

### Catch all exceptions — `Exception` base class
```python
try:
    risky_code()
except Exception as e:
    print(f"Something went wrong: {e}")
    print(f"Type: {type(e).__name__}")
```

> ⚠️ **Avoid bare `except:`** — it catches everything including `KeyboardInterrupt` and `SystemExit` which should never be silenced:
> ```python
> except:           # ❌ bad — catches EVERYTHING
>     pass
>
> except Exception as e:   # ✅ better — catches standard exceptions
>     handle(e)
> ```

---

## 5. `else` — Runs When No Exception Occurred

```python
try:
    result = 10 / 2
except ZeroDivisionError:
    print("Division error!")
else:
    print(f"Success! Result = {result}")   # runs only if no exception

# Output: Success! Result = 5.0
```

```python
# Practical use — reading a file
try:
    f = open("data.txt", "r")
except FileNotFoundError:
    print("File not found!")
else:
    content = f.read()    # only runs if file opened successfully
    print(content)
    f.close()
```

> **Interview tip:** `else` in try-except means "run this only if try succeeded" — keeps success path separate from error path.

---

## 6. `finally` — Always Runs

`finally` runs **no matter what** — exception or not, handled or not. Used for cleanup.

```python
try:
    result = 10 / 0
except ZeroDivisionError:
    print("Error caught!")
finally:
    print("This always runs — cleanup here")

# Output:
# Error caught!
# This always runs — cleanup here
```

```python
# finally runs even when exception is NOT caught
try:
    result = 10 / 0
finally:
    print("Cleanup!")   # runs before program crashes

# Output:
# Cleanup!
# ZeroDivisionError: division by zero
```

```python
# finally runs even with return inside try
def risky():
    try:
        return "from try"
    finally:
        print("finally runs!")   # runs before return

print(risky())
# finally runs!
# from try
```

**Real use — resource cleanup:**
```python
file = None
try:
    file = open("data.txt", "r")
    content = file.read()
except FileNotFoundError:
    print("File not found!")
except Exception as e:
    print(f"Error: {e}")
finally:
    if file:
        file.close()   # always close the file
        print("File closed.")
```

---

## 7. Full Structure — `try-except-else-finally`

```python
try:
    result = int(input("Enter a number: "))
    answer = 100 / result

except ValueError:
    print("Not a valid number!")

except ZeroDivisionError:
    print("Cannot divide by zero!")

except Exception as e:
    print(f"Unexpected error: {e}")

else:
    # runs ONLY if try succeeded — no exception at all
    print(f"Result: {answer}")

finally:
    # ALWAYS runs — cleanup
    print("Done.")
```

**Execution flow:**
```
try succeeds  → else → finally
try fails     → except → finally
except misses → finally → exception propagates up
```

---

## 8. `raise` — Raise an Exception Manually

```python
def divide(a, b):
    if b == 0:
        raise ZeroDivisionError("b must be non-zero")
    return a / b

try:
    print(divide(10, 0))
except ZeroDivisionError as e:
    print(f"Caught: {e}")
# Output: Caught: b must be non-zero
```

```python
# Validate input with raise
def set_age(age):
    if not isinstance(age, int):
        raise TypeError(f"Age must be int, got {type(age).__name__}")
    if age < 0 or age > 150:
        raise ValueError(f"Age {age} is out of valid range (0-150)")
    return age

try:
    set_age(-5)
except ValueError as e:
    print(f"ValueError: {e}")
# Output: ValueError: Age -5 is out of valid range (0-150)
```

### `raise` without argument — re-raise current exception
```python
def process(data):
    try:
        result = risky_operation(data)
    except Exception as e:
        print(f"Logging error: {e}")
        raise    # re-raises same exception — preserves traceback
```

---

## 9. Custom Exceptions

Create your own exception by inheriting from `Exception`.

```python
class InsufficientBalanceError(Exception):
    def __init__(self, balance, amount):
        self.balance = balance
        self.amount  = amount
        super().__init__(
            f"Cannot withdraw ₹{amount}. Balance is ₹{balance}."
        )

class BankAccount:
    def __init__(self, owner, balance):
        self.owner   = owner
        self.balance = balance

    def withdraw(self, amount):
        if amount > self.balance:
            raise InsufficientBalanceError(self.balance, amount)
        self.balance -= amount
        return self.balance

acc = BankAccount("AJ", 5000)

try:
    acc.withdraw(8000)
except InsufficientBalanceError as e:
    print(f"Error: {e}")
    print(f"Have ₹{e.balance}, tried to withdraw ₹{e.amount}")

# Output:
# Error: Cannot withdraw ₹8000. Balance is ₹5000.
# Have ₹5000, tried to withdraw ₹8000
```

**Exception hierarchy — always inherit from the right base:**
```python
class AppError(Exception):            # base for all app errors
    pass

class DatabaseError(AppError):        # category
    pass

class ConnectionError(DatabaseError): # specific
    pass
```

> **Interview tip:** Custom exceptions make errors meaningful. `InsufficientBalanceError` is clearer than a generic `ValueError`. They also let you attach extra data (like `balance` and `amount`) to the exception object.

---

## 10. `with` Statement — Context Manager

`with` automatically handles setup and cleanup — no need to write `finally` to close files.

```python
# Without with — manual cleanup
file = open("data.txt", "r")
try:
    content = file.read()
finally:
    file.close()   # must remember this

# With 'with' — automatic cleanup ✅
with open("data.txt", "r") as file:
    content = file.read()
# file is automatically closed when block exits — even if exception occurs
```

```python
# Multiple context managers
with open("input.txt", "r") as infile, open("output.txt", "w") as outfile:
    for line in infile:
        outfile.write(line.upper())
```

### Custom Context Manager
```python
class DatabaseConnection:
    def __init__(self, db_name):
        self.db_name = db_name

    def __enter__(self):
        print(f"Connecting to {self.db_name}...")
        return self

    def __exit__(self, exc_type, exc_val, exc_tb):
        print(f"Closing connection to {self.db_name}")
        return False   # False = don't suppress exceptions

    def query(self, sql):
        print(f"Running: {sql}")

with DatabaseConnection("students.db") as db:
    db.query("SELECT * FROM students")
# Connecting to students.db...
# Running: SELECT * FROM students
# Closing connection to students.db
```

---

## 11. `assert` Statement

`assert` tests a condition — raises `AssertionError` if False. Used for debugging.

```python
def calculate_average(marks):
    assert len(marks) > 0, "Marks list cannot be empty"
    return sum(marks) / len(marks)

try:
    avg = calculate_average([])
except AssertionError as e:
    print(f"AssertionError: {e}")
# Output: AssertionError: Marks list cannot be empty

avg = calculate_average([85, 90, 78])
print(avg)   # Output: 84.33...
```

> ⚠️ **Never use `assert` for input validation in production** — assertions can be disabled with `python -O` flag. Use `raise` with proper exceptions for real validation.

---

## 12. Exception Chaining

Link exceptions to show cause and effect.

```python
try:
    int("not_a_number")
except ValueError as e:
    raise RuntimeError("Failed to process data") from e

# Output shows both:
# ValueError: invalid literal for int() ...
# The above exception was the direct cause of:
# RuntimeError: Failed to process data
```

---

## 13. DSA Patterns — Exception Handling

### Safe Array Access
```python
def safe_get(lst, index, default=None):
    try:
        return lst[index]
    except IndexError:
        return default

arr = [10, 20, 30]
print(safe_get(arr, 1))      # Output: 20
print(safe_get(arr, 10))     # Output: None
print(safe_get(arr, 10, -1)) # Output: -1
```

### Safe Integer Conversion
```python
def safe_int(value, default=0):
    try:
        return int(value)
    except (ValueError, TypeError):
        return default

print(safe_int("42"))       # Output: 42
print(safe_int("hello"))    # Output: 0
print(safe_int(None, -1))   # Output: -1
```

### Input Validation Loop
```python
def get_valid_age():
    while True:
        try:
            age = int(input("Enter your age: "))
            if age < 0 or age > 120:
                raise ValueError("Age must be between 0 and 120")
            return age
        except ValueError as e:
            print(f"Invalid: {e}. Try again.")

age = get_valid_age()
```

---

## Quick Reference

```python
# FULL STRUCTURE
try:
    risky_code()
except SpecificError:
    handle_specific()
except (Error1, Error2) as e:
    handle_multiple(e)
except Exception as e:
    handle_any(e)
else:
    runs_if_no_exception()
finally:
    always_runs()

# RAISE
raise ValueError("message")        # raise new
raise                               # re-raise current
raise RuntimeError("msg") from e   # chain exceptions

# CUSTOM EXCEPTION
class MyError(Exception):
    def __init__(self, msg):
        super().__init__(msg)

# CONTEXT MANAGER
with open("file.txt") as f:
    data = f.read()

# ASSERT
assert condition, "error message"

# EXCEPTION INFO
except Exception as e:
    print(e)                    # message
    print(type(e).__name__)     # class name
    print(e.args)               # tuple of args

# EXCEPTION HIERARCHY
BaseException
├── SystemExit
├── KeyboardInterrupt
└── Exception
    ├── ValueError
    ├── TypeError
    ├── IndexError
    ├── KeyError
    ├── AttributeError
    ├── NameError
    ├── ZeroDivisionError
    ├── FileNotFoundError
    ├── ImportError
    └── RuntimeError
```

---

## Interview Short Answers

**Q: What is the difference between an error and an exception in Python?**
> Errors are serious problems the program usually cannot recover from — like `SyntaxError` and `IndentationError` which occur before the program even runs. Exceptions are runtime problems that can be caught and handled — like `ValueError`, `ZeroDivisionError`, and `KeyError`. All exceptions inherit from `BaseException`, and most user-handled ones from `Exception`.

**Q: What does `finally` do and when is it used?**
> The `finally` block always executes regardless of whether an exception occurred or was handled — even if there is a `return` inside the `try` block. It is used for cleanup code that must run no matter what — closing files, releasing database connections, freeing resources. It guarantees resources are never left open or locked.

**Q: What is the difference between `except Exception` and bare `except`?**
> Bare `except:` catches absolutely everything including `SystemExit` and `KeyboardInterrupt`, which should not normally be caught — it can make the program impossible to quit. `except Exception:` catches all standard exceptions but leaves system-level exceptions uncaught. Always prefer `except Exception as e` so you also have access to the exception details.

**Q: When does the `else` block run in try-except?**
> The `else` block runs only when the `try` block completes without raising any exception. It is useful for separating code that depends on try succeeding from the try block itself — keeping try small and focused on just the risky operation, and else for processing the result.

**Q: What is the difference between `raise` and plain `raise`?**
> Plain `raise` re-raises the current active exception — preserving the original traceback so the full call stack is visible. `raise e` raises the exception object `e` but resets the traceback to the current line, losing the original context. Use plain `raise` when logging an exception and letting it propagate unchanged.

**Q: What is a custom exception and why create one?**
> A custom exception is a class that inherits from `Exception` — created to represent errors specific to your application. They make error handling more precise, let you attach extra data to the error object, and make code more readable. For example, `InsufficientBalanceError` carrying the balance and attempted amount is far clearer than a generic `ValueError` in a banking application.

**Q: What is a context manager and what does `with` do?**
> A context manager is an object that defines `__enter__` and `__exit__` methods to manage setup and cleanup of resources. The `with` statement calls `__enter__` when entering the block and `__exit__` when leaving — even if an exception occurs. This guarantees resources like files and database connections are always properly closed without needing an explicit `finally` block.

**Q: What is the `assert` statement and when should you avoid it?**
> `assert condition, message` raises `AssertionError` if the condition is False. It is meant for debugging — verifying assumptions during development. Never use `assert` for input validation in production code because assertions can be disabled globally by running Python with the `-O` (optimize) flag, which strips all assert statements from the bytecode.
