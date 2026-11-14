# OOP in Python — Constructors and Methods
> OOP Series | File 02 of 08 | Interview Ready

---

## 1. What is a Constructor?

A constructor is a **special method that is automatically called when an object is created**. It initializes the object's attributes and sets up its initial state.

```
Student("AJ", 85)
       ↓
Python creates the object in memory
       ↓
__init__ is called automatically
       ↓
Object is ready to use
```

In Python, the constructor is the `__init__` method.

```python
class Student:
    def __init__(self, name, marks):   # constructor
        self.name  = name
        self.marks = marks
        print(f"Student {self.name} created!")

s1 = Student("AJ", 85)    # Output: Student AJ created!
s2 = Student("Rahul", 92) # Output: Student Rahul created!
```

---

## 2. Types of Constructors

### Type 1 — Default Constructor
No parameters (except `self`). Every object gets the same initial state.

```python
class Student:
    def __init__(self):          # default constructor — no parameters
        self.name  = "Unknown"
        self.marks = 0
        self.grade = "N/A"

s1 = Student()
s2 = Student()

print(s1.name)    # Output: Unknown
print(s2.marks)   # Output: 0

# Every object starts with the same default values
```

### Type 2 — Parameterized Constructor
Takes parameters — each object can be initialized with different values.

```python
class Student:
    def __init__(self, name, age, marks):   # parameterized constructor
        self.name  = name
        self.age   = age
        self.marks = marks

s1 = Student("AJ", 22, 85)
s2 = Student("Rahul", 21, 92)

print(s1.name, s1.marks)   # Output: AJ 85
print(s2.name, s2.marks)   # Output: Rahul 92
```

### Type 3 — Default Parameter Constructor
Combines both — parameters have default values, so you can call it with or without arguments.

```python
class Student:
    def __init__(self, name="Unknown", age=0, marks=0):
        self.name  = name
        self.age   = age
        self.marks = marks

s1 = Student()                    # uses all defaults
s2 = Student("AJ")                # name set, rest default
s3 = Student("Rahul", 21, 92)     # all values provided

print(s1.name, s1.marks)   # Output: Unknown 0
print(s2.name, s2.age)     # Output: AJ 0
print(s3.name, s3.marks)   # Output: Rahul 92
```

### Type 4 — Copy Constructor
Creates a new object as a copy of an existing object.

```python
class Student:
    def __init__(self, name, marks):
        self.name  = name
        self.marks = marks

    def copy(self):                     # copy constructor pattern
        return Student(self.name, self.marks)

s1 = Student("AJ", 85)
s2 = s1.copy()              # s2 is a copy of s1

print(s2.name, s2.marks)    # Output: AJ 85
print(s1 is s2)             # Output: False — different objects

# Modifying s2 doesn't affect s1
s2.marks = 99
print(s1.marks)   # Output: 85  ← unchanged
print(s2.marks)   # Output: 99
```

**Using Python's `copy` module:**
```python
import copy

class Student:
    def __init__(self, name, marks):
        self.name  = name
        self.marks = marks

s1 = Student("AJ", 85)

s2 = copy.copy(s1)      # shallow copy
s3 = copy.deepcopy(s1)  # deep copy (safe for nested objects)

print(s2.name)    # AJ
print(s1 is s2)   # False — different objects
```

---

## 3. `__new__` vs `__init__`

Python object creation happens in **two steps**:

```
Step 1: __new__  → allocates memory, creates the empty object
Step 2: __init__ → initializes the object with data
```

```python
class Student:
    def __new__(cls, name, marks):
        print(f"__new__ called — creating object in memory")
        instance = super().__new__(cls)   # allocate memory
        return instance                   # return the empty object

    def __init__(self, name, marks):
        print(f"__init__ called — filling object with data")
        self.name  = name
        self.marks = marks

s1 = Student("AJ", 85)
# Output:
# __new__ called — creating object in memory
# __init__ called — filling object with data
```

| | `__new__` | `__init__` |
|---|---|---|
| Purpose | Create the object | Initialize the object |
| First param | `cls` (the class) | `self` (the instance) |
| Returns | New object instance | Nothing (`None`) |
| Called | Before `__init__` | After `__new__` |
| Override? | Rarely — only for Singleton, immutable types | Commonly — set attributes |

> **Interview tip:** You almost never override `__new__`. It is used in advanced patterns like Singleton (only one instance allowed) and when subclassing immutable types like `int`, `str`, `tuple`. In 99% of cases, `__init__` is what you need.

---

## 4. Types of Methods

Python classes support four types of methods:

| Method Type | First Param | Decorator | Access |
|---|---|---|---|
| Instance method | `self` | None | Instance + class data |
| Class method | `cls` | `@classmethod` | Class data only |
| Static method | None | `@staticmethod` | Neither |
| Abstract method | `self` | `@abstractmethod` | Must be overridden |

---

## 5. Instance Methods

The most common type. Always takes `self` as first parameter. Can access and modify instance and class data.

```python
class BankAccount:
    interest_rate = 0.05   # class attribute

    def __init__(self, owner, balance):
        self.owner   = owner
        self.balance = balance

    def deposit(self, amount):          # instance method
        if amount > 0:
            self.balance += amount
            print(f"Deposited ₹{amount}. Balance: ₹{self.balance}")

    def withdraw(self, amount):
        if amount > self.balance:
            print("Insufficient balance")
        else:
            self.balance -= amount
            print(f"Withdrew ₹{amount}. Balance: ₹{self.balance}")

    def get_balance(self):
        return self.balance

    def apply_interest(self):
        interest = self.balance * BankAccount.interest_rate
        self.balance += interest
        print(f"Interest applied. New balance: ₹{self.balance:.2f}")

acc = BankAccount("AJ", 10000)
acc.deposit(5000)       # Output: Deposited ₹5000. Balance: ₹15000
acc.withdraw(3000)      # Output: Withdrew ₹3000. Balance: ₹12000
acc.apply_interest()    # Output: Interest applied. New balance: ₹12600.00
```

---

## 6. Class Methods — `@classmethod`

- Decorated with `@classmethod`
- Takes `cls` (the class) as first parameter, not `self`
- Can access and modify **class attributes**
- Cannot access instance attributes
- Called on the class, not an object

**Primary use: Alternative constructors — create objects from different input formats**

```python
class Student:
    school = "VTU"
    count  = 0

    def __init__(self, name, marks):
        self.name  = name
        self.marks = marks
        Student.count += 1

    # Alternative constructor — create from a string "AJ,85"
    @classmethod
    def from_string(cls, data_string):
        name, marks = data_string.split(",")
        return cls(name, int(marks))    # cls() = Student()

    # Alternative constructor — create from a dictionary
    @classmethod
    def from_dict(cls, data_dict):
        return cls(data_dict["name"], data_dict["marks"])

    # Modify class attribute
    @classmethod
    def change_school(cls, new_school):
        cls.school = new_school

    @classmethod
    def get_count(cls):
        return cls.count

# Normal creation
s1 = Student("AJ", 85)

# Alternative constructors
s2 = Student.from_string("Rahul,92")
s3 = Student.from_dict({"name": "Priya", "marks": 78})

print(s2.name, s2.marks)    # Output: Rahul 92
print(s3.name, s3.marks)    # Output: Priya 78
print(Student.get_count())  # Output: 3

Student.change_school("MIT")
print(Student.school)       # Output: MIT
```

---

## 7. Static Methods — `@staticmethod`

- Decorated with `@staticmethod`
- Takes **no** `self` or `cls` parameter
- Cannot access instance or class data
- Just a utility function logically grouped with the class
- Called on the class (or object, but class is preferred)

```python
class MathUtils:
    @staticmethod
    def add(a, b):
        return a + b

    @staticmethod
    def is_prime(n):
        if n < 2:
            return False
        for i in range(2, int(n ** 0.5) + 1):
            if n % i == 0:
                return False
        return True

    @staticmethod
    def factorial(n):
        if n == 0:
            return 1
        result = 1
        for i in range(1, n + 1):
            result *= i
        return result

# No need to create an object
print(MathUtils.add(3, 4))        # Output: 7
print(MathUtils.is_prime(29))     # Output: True
print(MathUtils.factorial(5))     # Output: 120
```

```python
class Student:
    def __init__(self, name, marks):
        self.name  = name
        self.marks = marks

    @staticmethod
    def validate_marks(marks):       # doesn't need self or cls
        return 0 <= marks <= 100

    def set_marks(self, marks):
        if Student.validate_marks(marks):  # static called from instance method
            self.marks = marks
        else:
            raise ValueError("Marks must be between 0 and 100")

s1 = Student("AJ", 85)
s1.set_marks(95)
print(s1.marks)   # Output: 95

s1.set_marks(150) # ❌ ValueError: Marks must be between 0 and 100
```

---

## 8. Getter and Setter Methods

Control how attributes are accessed and modified — add validation and logic.

### Manual Getter and Setter
```python
class Student:
    def __init__(self, name, marks):
        self.__name  = name    # private
        self.__marks = marks   # private

    # Getter
    def get_name(self):
        return self.__name

    # Getter
    def get_marks(self):
        return self.__marks

    # Setter with validation
    def set_marks(self, marks):
        if 0 <= marks <= 100:
            self.__marks = marks
        else:
            print("Invalid marks — must be 0 to 100")

    # Setter with validation
    def set_name(self, name):
        if isinstance(name, str) and len(name) > 0:
            self.__name = name
        else:
            print("Invalid name")

s1 = Student("AJ", 85)
print(s1.get_name())    # Output: AJ
print(s1.get_marks())   # Output: 85

s1.set_marks(95)
print(s1.get_marks())   # Output: 95

s1.set_marks(150)       # Output: Invalid marks — must be 0 to 100
```

### Pythonic Getter and Setter — `@property`
Better than manual get/set — access like an attribute, behaves like a method.

```python
class Student:
    def __init__(self, name, marks):
        self.__name  = name
        self.__marks = marks

    @property
    def name(self):              # getter — accessed as s1.name
        return self.__name

    @name.setter
    def name(self, value):       # setter — called as s1.name = "..."
        if isinstance(value, str) and len(value) > 0:
            self.__name = value
        else:
            raise ValueError("Name must be a non-empty string")

    @property
    def marks(self):
        return self.__marks

    @marks.setter
    def marks(self, value):
        if 0 <= value <= 100:
            self.__marks = value
        else:
            raise ValueError("Marks must be between 0 and 100")

    @property
    def grade(self):             # computed property — no setter needed
        if self.__marks >= 90: return "A"
        if self.__marks >= 75: return "B"
        if self.__marks >= 60: return "C"
        return "F"

s1 = Student("AJ", 85)

print(s1.name)      # Output: AJ    (calls getter)
print(s1.marks)     # Output: 85    (calls getter)
print(s1.grade)     # Output: B     (computed property)

s1.name  = "Gagan"  # calls setter
s1.marks = 92       # calls setter
print(s1.grade)     # Output: A

s1.marks = 150      # ❌ ValueError: Marks must be between 0 and 100
```

> **Interview tip:** `@property` is the Pythonic standard. Manual `get_name()` / `set_name()` is the Java style — avoid it in Python. The `@property` approach keeps the interface clean (`s1.name` not `s1.get_name()`) while still controlling access internally.

---

## 9. Destructor — `__del__`

Called automatically when an object is about to be destroyed (garbage collected).

```python
class DatabaseConnection:
    def __init__(self, host):
        self.host = host
        print(f"Connected to {self.host}")

    def query(self, sql):
        print(f"Running: {sql}")

    def __del__(self):
        print(f"Connection to {self.host} closed.")

# Object created
db = DatabaseConnection("localhost")   # Output: Connected to localhost
db.query("SELECT * FROM users")        # Output: Running: SELECT * FROM users

# Object deleted
del db    # Output: Connection to localhost closed.
```

```python
# __del__ is called when reference count drops to zero
class Student:
    def __init__(self, name):
        self.name = name

    def __del__(self):
        print(f"{self.name} cleaned up")

s1 = Student("AJ")
s2 = s1           # s2 also points to same object — 2 references

del s1            # reference count: 2 → 1  — __del__ NOT called yet
del s2            # reference count: 1 → 0  — __del__ called NOW
# Output: AJ cleaned up
```

> **Interview tip:** Don't rely on `__del__` for critical cleanup in production — Python's garbage collector doesn't guarantee exactly when it's called, especially with circular references. Use `with` statement and context managers (`__enter__`/`__exit__`) for reliable resource cleanup.

---

## 10. Method Chaining

Returning `self` from methods allows chaining multiple method calls on one line.

```python
class QueryBuilder:
    def __init__(self):
        self.query = "SELECT"
        self.conditions = []

    def select(self, columns):
        self.query += f" {columns}"
        return self                 # return self to enable chaining

    def from_table(self, table):
        self.query += f" FROM {table}"
        return self

    def where(self, condition):
        self.conditions.append(condition)
        return self

    def build(self):
        if self.conditions:
            self.query += " WHERE " + " AND ".join(self.conditions)
        return self.query

# Method chaining — clean and readable
result = (QueryBuilder()
          .select("name, marks")
          .from_table("students")
          .where("marks > 80")
          .where("age < 25")
          .build())

print(result)
# Output: SELECT name, marks FROM students WHERE marks > 80 AND age < 25
```

```python
# Simpler example
class Student:
    def __init__(self, name):
        self.name   = name
        self.marks  = 0
        self.grade  = ""

    def set_marks(self, marks):
        self.marks = marks
        return self

    def set_grade(self, grade):
        self.grade = grade
        return self

    def display(self):
        print(f"{self.name} — Marks: {self.marks}, Grade: {self.grade}")
        return self

# Chained
Student("AJ").set_marks(85).set_grade("B").display()
# Output: AJ — Marks: 85, Grade: B
```

---

## Quick Reference

```python
# CONSTRUCTOR TYPES
class MyClass:
    def __init__(self):              # default
        self.attr = "default"

    def __init__(self, val):         # parameterized
        self.attr = val

    def __init__(self, val="default"): # with default param
        self.attr = val

    @classmethod
    def from_string(cls, s):         # copy / alternative constructor
        return cls(s)

# __new__ vs __init__
def __new__(cls, *args):   # creates object — rarely overridden
    return super().__new__(cls)
def __init__(self, *args): # initializes object — commonly overridden
    self.attr = args[0]

# METHOD TYPES
def method(self):          # instance method — access self
@classmethod
def method(cls):           # class method — access cls
@staticmethod
def method():              # static method — no self/cls

# PROPERTY
@property
def attr(self): return self.__attr          # getter

@attr.setter
def attr(self, val): self.__attr = val      # setter

@attr.deleter
def attr(self): del self.__attr             # deleter

# DESTRUCTOR
def __del__(self): cleanup()

# METHOD CHAINING
def method(self):
    # do something
    return self    # return self to allow chaining
```

---

## Interview Short Answers

**Q: What are the types of constructors in Python?**
> Python has four constructor patterns. A default constructor takes no parameters and sets fixed initial values for all objects. A parameterized constructor takes arguments so each object can be initialized with different data. A default parameter constructor combines both — parameters have default values, so it works with or without arguments. A copy constructor creates a new object as a copy of an existing one, either manually or using Python's `copy` module. All use `__init__` as the underlying method.

**Q: What is the difference between `__new__` and `__init__`?**
> `__new__` is called first — it allocates memory and creates the empty object, receiving `cls` (the class) as its first argument and returning the new instance. `__init__` is called next — it initializes the object with data, receiving `self` (the new instance) as its first argument and returning nothing. In practice, you almost never override `__new__` — it is only needed for Singleton patterns or subclassing immutable types like `int` and `str`.

**Q: What is the difference between instance method, class method, and static method?**
> An instance method takes `self` as the first parameter and can access and modify both instance and class data — the most common type. A class method is decorated with `@classmethod`, takes `cls` as the first parameter, and can only access class-level data — commonly used as alternative constructors. A static method is decorated with `@staticmethod`, takes no implicit first parameter, and cannot access instance or class data — it is a utility function logically grouped with the class.

**Q: What is `@property` and why use it over manual getters and setters?**
> `@property` is a decorator that lets you define a method that is accessed like an attribute. Combined with `@attr.setter`, it gives you the control of a method with the clean syntax of attribute access. Instead of calling `s1.get_marks()` and `s1.set_marks(95)`, you write `s1.marks` and `s1.marks = 95`. It is the Pythonic standard because it keeps the public interface clean while still allowing validation and logic inside the method.

**Q: What is a destructor in Python and when is it called?**
> A destructor is the `__del__` method — called automatically when an object's reference count drops to zero and it is about to be garbage collected. It is used for cleanup tasks like closing file handles or database connections. However, Python does not guarantee exactly when `__del__` is called, especially in cases of circular references. For reliable resource cleanup, `with` statements and context managers using `__enter__` and `__exit__` are preferred.

**Q: What is method chaining?**
> Method chaining is a technique where each method returns `self`, allowing multiple method calls to be chained on a single line. It is used to build fluent, readable interfaces — common in query builders, configuration builders, and data processing pipelines. For example, `obj.set_name("AJ").set_marks(85).display()` works because each method returns the same object. Popular libraries like pandas use method chaining extensively.

**Q: What is a class method used for as an alternative constructor?**
> A class method can serve as an alternative constructor by creating and returning a new instance from a different input format. The standard `__init__` accepts specific arguments, but sometimes data arrives as a string, a dictionary, or a file. Using `@classmethod` with a name like `from_string()` or `from_dict()` lets you offer multiple ways to create an object cleanly, without overloading `__init__` with complex logic or many optional parameters.
