# OOP in Python — Polymorphism
> OOP Series | File 05 of 08 | Interview Ready

---

## 1. What is Polymorphism?

Polymorphism means **"many forms"** — the same interface (method name / operator) behaves differently depending on the object it acts on.

```
poly  =  many
morphism  =  forms

Same name, different behavior depending on the object.
```

**Real-world analogy:**
```
"speak()" means different things for different animals:
  Dog.speak()   → "Woof!"
  Cat.speak()   → "Meow!"
  Duck.speak()  → "Quack!"

Same method call → different output → Polymorphism
```

**Types of Polymorphism in Python:**
| Type | How it works |
|---|---|
| Duck Typing | Any object with the right method works — no type check needed |
| Method Overriding | Child redefines parent's method |
| Operator Overloading | Same operator (`+`, `==`, `<`) works on custom objects |
| Method Overloading | Python handles via default args / `*args` (no native overloading) |

---

## 2. Duck Typing

> *"If it walks like a duck and quacks like a duck, it's a duck."*

Python doesn't care about the **type** of an object — only whether it has the method being called. This is the foundation of Python's polymorphism.

```python
class Dog:
    def speak(self):
        return "Woof!"

class Cat:
    def speak(self):
        return "Meow!"

class Duck:
    def speak(self):
        return "Quack!"

class Person:
    def speak(self):
        return "Hello!"

# No common parent class needed — just the method name
def make_it_speak(animal):        # works with ANY object that has speak()
    print(animal.speak())

animals = [Dog(), Cat(), Duck(), Person()]
for a in animals:
    make_it_speak(a)
# Woof!
# Meow!
# Quack!
# Hello!
```

```python
# Duck typing with file-like objects
class FileWriter:
    def write(self, data):
        print(f"Writing to file: {data}")

class DatabaseWriter:
    def write(self, data):
        print(f"Inserting to DB: {data}")

class ConsoleWriter:
    def write(self, data):
        print(f"Console output: {data}")

def save_data(writer, data):     # any object with .write() works
    writer.write(data)

save_data(FileWriter(), "user_data")      # Writing to file: user_data
save_data(DatabaseWriter(), "user_data")  # Inserting to DB: user_data
save_data(ConsoleWriter(), "user_data")   # Console output: user_data
```

> **Key point:** Python doesn't require `isinstance()` checks before calling a method. If the object has the method, it works. This is why Python code is naturally flexible and polymorphic.

---

## 3. Polymorphism via Method Overriding

The most common form — child classes override a parent method and each gives their own version.

```python
class Shape:
    def area(self):
        raise NotImplementedError("Subclasses must implement area()")

    def describe(self):
        print(f"{self.__class__.__name__} — Area: {self.area():.2f}")


class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius

    def area(self):                      # overrides Shape.area
        return 3.14159 * self.radius ** 2


class Rectangle(Shape):
    def __init__(self, width, height):
        self.width  = width
        self.height = height

    def area(self):                      # overrides Shape.area
        return self.width * self.height


class Triangle(Shape):
    def __init__(self, base, height):
        self.base   = base
        self.height = height

    def area(self):                      # overrides Shape.area
        return 0.5 * self.base * self.height


shapes = [Circle(7), Rectangle(4, 6), Triangle(5, 8)]

for shape in shapes:
    shape.describe()                     # same call → different behavior
# Circle — Area: 153.94
# Rectangle — Area: 24.00
# Triangle — Area: 20.00

# Works with built-in functions too
print(max(shapes, key=lambda s: s.area()))  # finds largest shape
```

---

## 4. Polymorphism with Built-in Functions

Python's built-in functions like `len()`, `str()`, `repr()`, `abs()`, `iter()` are themselves polymorphic — they call dunder methods on the object.

```python
# len() calls __len__
print(len("hello"))       # 5   — str.__len__
print(len([1, 2, 3]))     # 3   — list.__len__
print(len({"a": 1}))      # 1   — dict.__len__

class Playlist:
    def __init__(self, songs):
        self.songs = songs

    def __len__(self):
        return len(self.songs)

p = Playlist(["Song A", "Song B", "Song C"])
print(len(p))             # 3  ← polymorphic — same len() call


# str() calls __str__
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __str__(self):
        return f"Point({self.x}, {self.y})"

    def __repr__(self):
        return f"Point(x={self.x}, y={self.y})"

p = Point(3, 4)
print(str(p))             # Point(3, 4)    — calls __str__
print(repr(p))            # Point(x=3, y=4) — calls __repr__
print(p)                  # Point(3, 4)    — print calls __str__
```

---

## 5. Operator Overloading

Python allows custom classes to define behavior for operators (`+`, `-`, `*`, `==`, `<`, `>`, etc.) using **dunder methods**.

```python
class Vector:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __add__(self, other):            # v1 + v2
        return Vector(self.x + other.x, self.y + other.y)

    def __sub__(self, other):            # v1 - v2
        return Vector(self.x - other.x, self.y - other.y)

    def __mul__(self, scalar):           # v1 * 3
        return Vector(self.x * scalar, self.y * scalar)

    def __eq__(self, other):             # v1 == v2
        return self.x == other.x and self.y == other.y

    def __lt__(self, other):             # v1 < v2  (by magnitude)
        return self.magnitude() < other.magnitude()

    def __abs__(self):                   # abs(v1)
        return self.magnitude()

    def magnitude(self):
        return (self.x ** 2 + self.y ** 2) ** 0.5

    def __str__(self):
        return f"Vector({self.x}, {self.y})"

    def __repr__(self):
        return f"Vector(x={self.x}, y={self.y})"


v1 = Vector(2, 3)
v2 = Vector(1, 4)

print(v1 + v2)       # Vector(3, 7)
print(v1 - v2)       # Vector(1, -1)
print(v1 * 3)        # Vector(6, 9)
print(v1 == v2)      # False
print(v1 < v2)       # False (magnitude 3.6 vs 4.1)
print(abs(v1))       # 3.605...

vectors = [Vector(5, 0), Vector(1, 1), Vector(3, 4)]
print(sorted(vectors))  # sorted by magnitude — uses __lt__
```

**Common dunder methods for operator overloading:**

| Operator | Dunder Method | Example |
|---|---|---|
| `+` | `__add__` | `a + b` |
| `-` | `__sub__` | `a - b` |
| `*` | `__mul__` | `a * b` |
| `/` | `__truediv__` | `a / b` |
| `//` | `__floordiv__` | `a // b` |
| `%` | `__mod__` | `a % b` |
| `**` | `__pow__` | `a ** b` |
| `==` | `__eq__` | `a == b` |
| `!=` | `__ne__` | `a != b` |
| `<` | `__lt__` | `a < b` |
| `<=` | `__le__` | `a <= b` |
| `>` | `__gt__` | `a > b` |
| `>=` | `__ge__` | `a >= b` |
| `len()` | `__len__` | `len(a)` |
| `str()` | `__str__` | `str(a)` |
| `abs()` | `__abs__` | `abs(a)` |
| `[]` | `__getitem__` | `a[key]` |
| `in` | `__contains__` | `x in a` |

---

## 6. Method Overloading (Python Style)

Python does NOT support traditional method overloading (same name, different parameter types) like Java/C++. Instead, Python uses **default arguments** or `*args` to achieve the same result.

```python
# Traditional approach — default arguments
class Calculator:
    def add(self, a, b=0, c=0):        # simulates overloading
        return a + b + c

calc = Calculator()
print(calc.add(5))           # 5
print(calc.add(5, 3))        # 8
print(calc.add(5, 3, 2))     # 10


# Flexible approach — *args
class MathOps:
    def add(self, *args):
        return sum(args)

    def multiply(self, *args):
        result = 1
        for n in args: result *= n
        return result

m = MathOps()
print(m.add(1, 2))           # 3
print(m.add(1, 2, 3, 4, 5))  # 15
print(m.multiply(2, 3, 4))   # 24


# Type-based dispatch (advanced — using isinstance)
class Processor:
    def process(self, data):
        if isinstance(data, list):
            return f"Processing list of {len(data)} items"
        elif isinstance(data, str):
            return f"Processing string: '{data}'"
        elif isinstance(data, int):
            return f"Processing number: {data * 2}"

p = Processor()
print(p.process([1, 2, 3]))   # Processing list of 3 items
print(p.process("hello"))     # Processing string: 'hello'
print(p.process(10))          # Processing number: 20
```

---

## 7. Polymorphism with `ABC` (Enforced Interface)

Using `ABC` ensures all subclasses implement required methods — a formal polymorphic contract.

```python
from abc import ABC, abstractmethod

class Payment(ABC):
    @abstractmethod
    def pay(self, amount):
        pass

    @abstractmethod
    def refund(self, amount):
        pass

    def receipt(self, amount):           # concrete — shared by all
        print(f"Receipt: ₹{amount} processed via {self.__class__.__name__}")


class CreditCard(Payment):
    def pay(self, amount):
        print(f"Paid ₹{amount} via Credit Card")

    def refund(self, amount):
        print(f"Refunded ₹{amount} to Credit Card")


class UPI(Payment):
    def pay(self, amount):
        print(f"Paid ₹{amount} via UPI")

    def refund(self, amount):
        print(f"Refunded ₹{amount} to UPI wallet")


class Cash(Payment):
    def pay(self, amount):
        print(f"Paid ₹{amount} in Cash")

    def refund(self, amount):
        print(f"Returned ₹{amount} cash")


# Polymorphic usage — same interface, different implementation
def process_payment(payment_method, amount):
    payment_method.pay(amount)
    payment_method.receipt(amount)

methods = [CreditCard(), UPI(), Cash()]
for method in methods:
    process_payment(method, 500)
    print()
# Paid ₹500 via Credit Card
# Receipt: ₹500 processed via CreditCard
# ...
```

---

## 8. `__iter__` and `__next__` — Polymorphic Iteration

Python's `for` loop is polymorphic — it works on any object that implements `__iter__` and `__next__`.

```python
class CountDown:
    def __init__(self, start):
        self.current = start

    def __iter__(self):
        return self

    def __next__(self):
        if self.current <= 0:
            raise StopIteration
        val = self.current
        self.current -= 1
        return val

for n in CountDown(5):
    print(n, end=" ")     # 5 4 3 2 1


class EvenNumbers:
    def __init__(self, limit):
        self.limit   = limit
        self.current = 0

    def __iter__(self):
        return self

    def __next__(self):
        self.current += 2
        if self.current > self.limit:
            raise StopIteration
        return self.current

print(list(EvenNumbers(10)))   # [2, 4, 6, 8, 10]
```

---

## 9. DSA Pattern — Polymorphic Sort Key

```python
class Student:
    def __init__(self, name, gpa, age):
        self.name = name
        self.gpa  = gpa
        self.age  = age

    def __lt__(self, other):             # default sort by GPA descending
        return self.gpa > other.gpa

    def __eq__(self, other):
        return self.gpa == other.gpa

    def __str__(self):
        return f"{self.name}(GPA={self.gpa})"

    def __repr__(self):
        return self.__str__()


students = [
    Student("AJ",    8.5, 22),
    Student("Rahul", 9.0, 23),
    Student("Priya", 7.8, 21),
    Student("Neha",  9.0, 22),
]

# sort() uses __lt__ — polymorphic
students.sort()
print(students)   # [Rahul(GPA=9.0), Neha(GPA=9.0), AJ(GPA=8.5), Priya(GPA=7.8)]

# Custom sort key — different polymorphic behavior
by_age  = sorted(students, key=lambda s: s.age)
by_name = sorted(students, key=lambda s: s.name)
print([s.name for s in by_age])    # ['Priya', 'AJ', 'Neha', 'Rahul']
print([s.name for s in by_name])   # ['AJ', 'Neha', 'Priya', 'Rahul']
```

---

## Quick Reference

```python
# DUCK TYPING — no type check needed
def process(obj):
    obj.method()     # works if obj has .method(), regardless of type

# METHOD OVERRIDING — same name, different behavior per class
class Parent:
    def greet(self): return "Hello from Parent"

class Child(Parent):
    def greet(self): return "Hello from Child"   # overrides

# OPERATOR OVERLOADING
class MyClass:
    def __add__(self, other): ...    # a + b
    def __eq__(self, other):  ...    # a == b
    def __lt__(self, other):  ...    # a < b  (also enables sorted())
    def __len__(self):        ...    # len(a)
    def __str__(self):        ...    # str(a), print(a)
    def __getitem__(self, k): ...    # a[k]
    def __contains__(self, x):...   # x in a

# METHOD OVERLOADING (Python style)
def method(self, a, b=None, *args): ...   # default args
def method(self, *args): ...              # variable args

# POLYMORPHIC LOOP
for item in collection:   # works if __iter__ and __next__ defined
    ...
```

---

## Interview Short Answers

**Q: What is polymorphism? Give a real example.**
> Polymorphism means the same interface behaves differently depending on the object. A real example: `len([1,2,3])` returns 3, `len("hello")` returns 5, `len({"a":1})` returns 1 — the same `len()` function works on completely different types. Under the hood, it calls the `__len__` method of each object. In custom classes: a list of shapes with `Circle`, `Rectangle`, and `Triangle` all have an `area()` method, but each computes differently. Calling `shape.area()` on each gives the right result without checking the type.

**Q: What is duck typing?**
> Duck typing is Python's approach to polymorphism based on behavior rather than type. If an object has the method being called, it works — Python doesn't check whether the object is an instance of a particular class. The name comes from the phrase "if it walks like a duck and quacks like a duck, it's a duck." Practically, a function that calls `obj.write(data)` works with a file object, a database connection, or a custom logger — as long as each has a `write()` method.

**Q: What is operator overloading?**
> Operator overloading lets custom classes define behavior for Python's built-in operators using dunder methods. For example, defining `__add__` on a `Vector` class makes `v1 + v2` work. Defining `__eq__` makes `==` compare by value instead of identity. Defining `__lt__` makes the class work with `sorted()` and `min()/max()`. It makes custom objects feel native and intuitive — a `Fraction` class with `__add__` lets you write `Fraction(1,2) + Fraction(1,3)` naturally.

**Q: Does Python support method overloading?**
> Python does not support traditional method overloading (same method name, different parameter types) like Java or C++. If you define the same method name twice, the second definition simply replaces the first. Python achieves the same effect using default parameter values, `*args`, or `**kwargs` — one method handles multiple call signatures. You can also use `isinstance()` inside the method to dispatch behavior based on input type.

**Q: What is the difference between method overriding and method overloading?**
> Method overriding happens between a parent and child class — the child redefines a method inherited from the parent with the same name and signature. It is a runtime concept (dynamic dispatch). Method overloading is defining multiple methods with the same name but different parameters in the same class — Python doesn't support this natively, but achieves it with default arguments or `*args`. Overriding is about inheritance; overloading is about multiple call signatures.

**Q: How does Python's `for` loop use polymorphism?**
> Python's `for` loop works on any object that implements `__iter__` (returns an iterator) and `__next__` (returns the next value and raises `StopIteration` when done). It calls these methods implicitly — it doesn't care whether the object is a list, a tuple, a custom class, or a generator. This is polymorphism: the same `for` loop syntax works uniformly across any iterable object.

**Q: What is the difference between polymorphism and inheritance?**
> Inheritance is a mechanism — a child class reuses code from a parent class. Polymorphism is a behavior — the same method call works differently on different objects. Inheritance often enables polymorphism (child overrides parent methods), but polymorphism doesn't require inheritance. Duck typing in Python is polymorphism without inheritance — completely unrelated classes can be used interchangeably if they share the same method names. Inheritance is about code reuse; polymorphism is about interface flexibility.
