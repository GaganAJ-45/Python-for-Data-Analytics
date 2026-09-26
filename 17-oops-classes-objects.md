# Object-Oriented Programming in Python

## 1. What is OOP?

Object-Oriented Programming is a programming paradigm that organizes code around **objects** rather than functions and logic. An object bundles **data (attributes)** and **behavior (methods)** together.

**4 Pillars of OOP:**
```
1. Encapsulation  → bundling data and methods, hiding internal details
2. Inheritance    → one class reusing properties of another
3. Polymorphism   → same interface, different behavior
4. Abstraction    → hiding complexity, showing only what's needed
```

**Why OOP?**
- Models real-world entities naturally
- Code is reusable, modular, and maintainable
- Easier to scale large projects
- Reduces code repetition

---

## 2. Class and Object

A **class** is a blueprint. An **object** is an instance created from that blueprint.

```
Class  → blueprint (like a house plan)
Object → actual instance (the house built from the plan)
```

```python
# Define a class
class Student:
    pass

# Create objects (instances)
s1 = Student()
s2 = Student()

print(type(s1))      # Output: <class '__main__.Student'>
print(s1 == s2)      # Output: False — different objects
print(id(s1) == id(s2))  # Output: False — different memory addresses
```

---

## 3. `__init__` — Constructor

`__init__` is called **automatically** when an object is created. It initializes the object's attributes.
or `__init__` is special method in python it initializes an object when its created. Its called automatically when create a new instance of a class

```python
class Student:
    def __init__(self, name, age, marks):
        self.name  = name     # instance attribute
        self.age   = age
        self.marks = marks

# Create objects
s1 = Student("AJ", 22, 85)
s2 = Student("Rahul", 21, 92)

print(s1.name)    # Output: AJ
print(s2.marks)   # Output: 92
```

> **`self` explained:** `self` refers to the current object being created or used. It is always the first parameter of instance methods. Python passes it automatically — you never pass it manually when calling the method.

```python
# What 'self' actually does
s1 = Student("AJ", 22, 85)
# Python internally calls: Student.__init__(s1, "AJ", 22, 85)
# self = s1
```

---

## 4. Instance Attributes vs Class Attributes

### Instance Attributes
Belong to **each object individually** — defined inside `__init__` using `self`.

```python
class Student:
    def __init__(self, name, marks):
        self.name  = name    # each object has its own name
        self.marks = marks   # each object has its own marks

s1 = Student("AJ", 85)
s2 = Student("Rahul", 92)

print(s1.name)   # AJ
print(s2.name)   # Rahul  — different from s1
```

### Class Attributes
Belong to the **class itself** — shared by all objects.

```python
class Student:
    school = "VTU"    # class attribute — shared by all

    def __init__(self, name):
        self.name = name  # instance attribute

s1 = Student("AJ")
s2 = Student("Rahul")

print(s1.school)   # Output: VTU
print(s2.school)   # Output: VTU
print(Student.school)  # Output: VTU  — access via class name

# Change class attribute — affects ALL objects
Student.school = "MIT"
print(s1.school)   # Output: MIT
print(s2.school)   # Output: MIT
```

> **Interview tip:** If you set `self.school = "MIT"` inside an object, it creates a new **instance attribute** that shadows the class attribute for that object only. The class attribute remains unchanged.

---

## 5. Instance Methods

Methods are functions defined inside a class. Instance methods always take `self` as first parameter.

```python
class Student:
    def __init__(self, name, marks):
        self.name  = name
        self.marks = marks

    def display(self):
        print(f"Name: {self.name}, Marks: {self.marks}")

    def grade(self):
        if self.marks >= 90:
            return "A"
        elif self.marks >= 75:
            return "B"
        else:
            return "C"

    def update_marks(self, new_marks):
        self.marks = new_marks

s1 = Student("AJ", 85)
s1.display()                  # Output: Name: AJ, Marks: 85
print(s1.grade())             # Output: B
s1.update_marks(95)
print(s1.grade())             # Output: A
```

---

## 6. `__str__` and `__repr__` — String Representation

### `__str__` — human-readable string (for `print()`)
```python
class Student:
    def __init__(self, name, marks):
        self.name  = name
        self.marks = marks

    def __str__(self):
        return f"Student(name={self.name}, marks={self.marks})"

s1 = Student("AJ", 85)
print(s1)        # Output: Student(name=AJ, marks=85)
print(str(s1))   # Output: Student(name=AJ, marks=85)
```

### `__repr__` — developer-readable string (for debugging)
```python
def __repr__(self):
    return f"Student('{self.name}', {self.marks})"

# repr() is shown in REPL and debugging
repr(s1)   # "Student('AJ', 85)"
```

> **Interview tip:** `__str__` is for end users — readable output. `__repr__` is for developers — should ideally be a string that can recreate the object. If only `__repr__` is defined, Python uses it for `print()` too.

---

## 7. Encapsulation

Bundling data and methods together, and **restricting direct access** to internal details.

### Access Modifiers (by convention)

| Convention | Type | Access |
|---|---|---|
| `name` | Public | Accessible everywhere |
| `_name` | Protected | Accessible but "handle with care" |
| `__name` | Private | Name mangled — not directly accessible |

```python
class BankAccount:
    def __init__(self, owner, balance):
        self.owner     = owner       # public
        self._account  = "ACC001"    # protected — convention only
        self.__balance = balance     # private — name mangled

    def deposit(self, amount):
        if amount > 0:
            self.__balance += amount

    def withdraw(self, amount):
        if 0 < amount <= self.__balance:
            self.__balance -= amount
        else:
            print("Insufficient balance")

    def get_balance(self):          # getter method
        return self.__balance

acc = BankAccount("AJ", 10000)
print(acc.owner)              # Output: AJ  (public)
print(acc._account)           # Output: ACC001  (works but not recommended)
print(acc.__balance)          # ❌ AttributeError — private

# Access private via name mangling
print(acc._BankAccount__balance)   # Output: 10000  (not recommended)

# Correct way — use getter
print(acc.get_balance())      # Output: 10000

acc.deposit(5000)
print(acc.get_balance())      # Output: 15000

acc.withdraw(3000)
print(acc.get_balance())      # Output: 12000
```

### Property — Pythonic getter/setter

```python
class Circle:
    def __init__(self, radius):
        self.__radius = radius

    @property
    def radius(self):             # getter
        return self.__radius

    @radius.setter
    def radius(self, value):      # setter
        if value < 0:
            raise ValueError("Radius cannot be negative")
        self.__radius = value

    @property
    def area(self):               # computed property
        return 3.14159 * self.__radius ** 2

c = Circle(5)
print(c.radius)    # Output: 5   (calls getter)
print(c.area)      # Output: 78.53975

c.radius = 10      # calls setter
print(c.radius)    # Output: 10

c.radius = -1      # ❌ ValueError: Radius cannot be negative
```

> **Interview tip:** `@property` is the Pythonic way to implement getters and setters. It lets you access methods like attributes (`c.radius` not `c.get_radius()`), keeping the interface clean while controlling access internally.

---

## 8. Inheritance

A class (**child**) inherits attributes and methods from another class (**parent**), allowing code reuse and extension.

```python
# Parent class
class Animal:
    def __init__(self, name, sound):
        self.name  = name
        self.sound = sound

    def speak(self):
        print(f"{self.name} says {self.sound}")

    def eat(self):
        print(f"{self.name} is eating")

# Child class — inherits from Animal
class Dog(Animal):
    def __init__(self, name):
        super().__init__(name, "Woof")   # call parent __init__
        self.tricks = []

    def learn_trick(self, trick):
        self.tricks.append(trick)
        print(f"{self.name} learned {trick}")

class Cat(Animal):
    def __init__(self, name):
        super().__init__(name, "Meow")

d = Dog("Bruno")
d.speak()                    # Output: Bruno says Woof  (inherited)
d.eat()                      # Output: Bruno is eating  (inherited)
d.learn_trick("sit")         # Output: Bruno learned sit  (own method)

c = Cat("Whiskers")
c.speak()                    # Output: Whiskers says Meow
```

### `super()` — Call Parent's Method

```python
class Vehicle:
    def __init__(self, brand, speed):
        self.brand = brand
        self.speed = speed

    def describe(self):
        print(f"{self.brand} — max speed: {self.speed} km/h")

class ElectricCar(Vehicle):
    def __init__(self, brand, speed, battery):
        super().__init__(brand, speed)   # call parent __init__
        self.battery = battery

    def describe(self):
        super().describe()              # call parent method
        print(f"Battery: {self.battery} kWh")

tesla = ElectricCar("Tesla", 250, 100)
tesla.describe()
# Tesla — max speed: 250 km/h
# Battery: 100 kWh
```

### Types of Inheritance

```python
# Single inheritance
class B(A): pass

# Multiple inheritance
class C(A, B): pass

# Multilevel inheritance
class A: pass
class B(A): pass
class C(B): pass    # C inherits from B which inherits from A

# Hierarchical
class A: pass
class B(A): pass
class C(A): pass    # both B and C inherit from A
```

### `isinstance()` and `issubclass()`
```python
d = Dog("Bruno")
print(isinstance(d, Dog))      # Output: True
print(isinstance(d, Animal))   # Output: True  — Dog IS an Animal
print(isinstance(d, Cat))      # Output: False

print(issubclass(Dog, Animal)) # Output: True
print(issubclass(Cat, Dog))    # Output: False
```

---

## 9. Polymorphism

**Same interface, different behavior** — the same method name works differently depending on which class's object calls it.

### Method Overriding
Child class provides its own version of a parent's method.

```python
class Shape:
    def area(self):
        return 0

class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius

    def area(self):                         # overrides parent
        return 3.14159 * self.radius ** 2

class Rectangle(Shape):
    def __init__(self, width, height):
        self.width  = width
        self.height = height

    def area(self):                         # overrides parent
        return self.width * self.height

class Triangle(Shape):
    def __init__(self, base, height):
        self.base   = base
        self.height = height

    def area(self):
        return 0.5 * self.base * self.height

# Polymorphism in action
shapes = [Circle(5), Rectangle(4, 6), Triangle(3, 8)]

for shape in shapes:
    print(f"{shape.__class__.__name__}: area = {shape.area():.2f}")
# Circle: area = 78.54
# Rectangle: area = 24.00
# Triangle: area = 12.00
```

### Duck Typing
"If it walks like a duck and quacks like a duck, it's a duck." Python doesn't check the type — just whether the method exists.

```python
class Dog:
    def speak(self):
        return "Woof!"

class Cat:
    def speak(self):
        return "Meow!"

class Robot:
    def speak(self):
        return "Beep boop!"

# Works for any object with a speak() method — no inheritance needed
animals = [Dog(), Cat(), Robot()]
for a in animals:
    print(a.speak())
# Woof!
# Meow!
# Beep boop!
```

### Operator Overloading
Define how operators work with your class using dunder methods.

```python
class Vector:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __add__(self, other):
        return Vector(self.x + other.x, self.y + other.y)

    def __str__(self):
        return f"Vector({self.x}, {self.y})"

    def __len__(self):
        return int((self.x**2 + self.y**2) ** 0.5)

v1 = Vector(1, 2)
v2 = Vector(3, 4)
v3 = v1 + v2          # calls __add__
print(v3)             # Output: Vector(4, 6)
print(len(v1))        # Output: 2  (calls __len__)
```

---

## 10. Abstraction

Hiding complex implementation details and showing only the essential interface.

### Abstract Base Class using `abc` module

```python
from abc import ABC, abstractmethod

class Shape(ABC):           # abstract class — cannot be instantiated
    @abstractmethod
    def area(self):         # abstract method — must be implemented
        pass

    @abstractmethod
    def perimeter(self):
        pass

    def describe(self):     # concrete method — shared by all
        print(f"Area: {self.area()}, Perimeter: {self.perimeter()}")

class Circle(Shape):
    def __init__(self, r):
        self.r = r

    def area(self):
        return 3.14159 * self.r ** 2

    def perimeter(self):
        return 2 * 3.14159 * self.r

class Rectangle(Shape):
    def __init__(self, w, h):
        self.w = w
        self.h = h

    def area(self):
        return self.w * self.h

    def perimeter(self):
        return 2 * (self.w + self.h)

# Shape()      # ❌ TypeError — cannot instantiate abstract class
c = Circle(5)
c.describe()   # Output: Area: 78.53975, Perimeter: 31.4159

r = Rectangle(4, 6)
r.describe()   # Output: Area: 24, Perimeter: 20
```

---

## 11. Class Methods and Static Methods

### `@classmethod` — works with the class, not the instance
Receives `cls` (the class itself) instead of `self`. Used as alternative constructors.

```python
class Student:
    school = "VTU"

    def __init__(self, name, marks):
        self.name  = name
        self.marks = marks

    @classmethod
    def from_string(cls, data):         # alternative constructor
        name, marks = data.split(",")
        return cls(name, int(marks))    # creates new instance

    @classmethod
    def change_school(cls, new_school):
        cls.school = new_school

s1 = Student("AJ", 85)
s2 = Student.from_string("Rahul,92")   # create from string
print(s2.name, s2.marks)               # Output: Rahul 92

Student.change_school("MIT")
print(Student.school)                  # Output: MIT
```

### `@staticmethod` — independent utility function
No `self` or `cls`. Doesn't access class or instance data. Just a utility function grouped with the class.

```python
class MathUtils:
    @staticmethod
    def add(a, b):
        return a + b

    @staticmethod
    def is_prime(n):
        if n < 2: return False
        for i in range(2, int(n**0.5) + 1):
            if n % i == 0: return False
        return True

print(MathUtils.add(3, 4))       # Output: 7
print(MathUtils.is_prime(29))    # Output: True
# No need to create an instance
```

| | Instance Method | Class Method | Static Method |
|---|---|---|---|
| First param | `self` | `cls` | None |
| Access instance | ✅ | ❌ | ❌ |
| Access class | ✅ | ✅ | ❌ |
| Use for | Instance behavior | Alternative constructors | Utility functions |

---

## 12. Dunder (Magic) Methods

Special methods with double underscores — Python calls them automatically.

```python
class Book:
    def __init__(self, title, pages):
        self.title = title
        self.pages = pages

    def __str__(self):       # print(obj)
        return f"'{self.title}' ({self.pages} pages)"

    def __repr__(self):      # repr(obj)
        return f"Book('{self.title}', {self.pages})"

    def __len__(self):       # len(obj)
        return self.pages

    def __eq__(self, other): # obj1 == obj2
        return self.title == other.title

    def __lt__(self, other): # obj1 < obj2 (for sorting)
        return self.pages < other.pages

    def __add__(self, other): # obj1 + obj2
        return Book(f"{self.title} & {other.title}",
                    self.pages + other.pages)

b1 = Book("Python", 300)
b2 = Book("DSA", 500)

print(b1)           # Output: 'Python' (300 pages)
print(len(b1))      # Output: 300
print(b1 == b2)     # Output: False
print(b1 < b2)      # Output: True
print(b1 + b2)      # Output: 'Python & DSA' (800 pages)

books = [b2, b1]
print(sorted(books))  # sorts using __lt__
```

**Common dunder methods:**

| Method | Called when |
|---|---|
| `__init__` | `obj = Class()` |
| `__str__` | `print(obj)` |
| `__repr__` | `repr(obj)` |
| `__len__` | `len(obj)` |
| `__eq__` | `obj1 == obj2` |
| `__lt__` | `obj1 < obj2` |
| `__add__` | `obj1 + obj2` |
| `__getitem__` | `obj[key]` |
| `__setitem__` | `obj[key] = val` |
| `__contains__` | `x in obj` |
| `__iter__` | `for x in obj` |
| `__del__` | object deleted |

---

## 13. MRO — Method Resolution Order

When using multiple inheritance, Python follows MRO to decide which method to call.

```python
class A:
    def greet(self):
        print("Hello from A")

class B(A):
    def greet(self):
        print("Hello from B")

class C(A):
    def greet(self):
        print("Hello from C")

class D(B, C):   # multiple inheritance
    pass

d = D()
d.greet()   # Output: Hello from B

# Check MRO
print(D.__mro__)
# (<class 'D'>, <class 'B'>, <class 'C'>, <class 'A'>, <class 'object'>)
```

> **MRO follows C3 linearization algorithm** — checks left to right, depth first. Python searches D → B → C → A → object. Always mention `__mro__` or `mro()` when explaining multiple inheritance in interviews.

---

## Quick Reference

```python
# CLASS DEFINITION
class ClassName:
    class_attr = value          # class attribute

    def __init__(self, params): # constructor
        self.attr = value       # instance attribute

    def method(self):           # instance method
        pass

    @classmethod
    def class_method(cls):      # class method
        pass

    @staticmethod
    def static_method():        # static method
        pass

# CREATE OBJECT
obj = ClassName(args)

# ACCESS
obj.attr                        # instance attribute
ClassName.class_attr            # class attribute
obj.method()                    # instance method

# INHERITANCE
class Child(Parent):
    def __init__(self):
        super().__init__()      # call parent constructor

    def method(self):           # override parent method
        super().method()        # call parent method too

# CHECKS
isinstance(obj, Class)          # is obj an instance of Class?
issubclass(Child, Parent)       # is Child a subclass of Parent?

# ENCAPSULATION
self.name    # public
self._name   # protected (convention)
self.__name  # private (name mangled to _Class__name)

@property
def name(self): return self.__name

@name.setter
def name(self, val): self.__name = val

# ABSTRACT CLASS
from abc import ABC, abstractmethod
class MyABC(ABC):
    @abstractmethod
    def must_implement(self): pass

# DUNDER METHODS
__init__  __str__  __repr__  __len__
__eq__  __lt__  __add__  __contains__
```

---

## Interview Short Answers

**Q: What are the 4 pillars of OOP?**
> The four pillars are Encapsulation — bundling data and methods while hiding internal details. Inheritance — a child class reusing and extending a parent class. Polymorphism — the same method name behaving differently depending on the object. Abstraction — hiding complexity and exposing only essential interfaces through abstract classes and methods.

**Q: What is the difference between a class and an object?**
> A class is a blueprint that defines attributes and methods. An object is an instance created from that blueprint with its own specific data. For example, `Student` is the class, and `s1 = Student("AJ", 22)` creates an object with name "AJ" and age 22. Multiple objects can be created from the same class, each independent.

**Q: What is `self` in Python?**
> `self` refers to the current instance of the class. It is always the first parameter of instance methods and is passed automatically by Python when you call a method on an object. Through `self`, each object accesses its own attributes and methods — it is what makes instance data unique to each object.

**Q: What is the difference between instance attributes and class attributes?**
> Instance attributes are defined inside `__init__` using `self` and belong to each individual object — different objects have different values. Class attributes are defined directly in the class body and are shared by all objects of that class. Modifying a class attribute through the class name affects all objects. Setting it on an instance creates a new instance attribute that shadows the class attribute for that object only.

**Q: What is the difference between `@classmethod` and `@staticmethod`?**
> A class method receives `cls` (the class itself) as the first argument and can access and modify class-level data. It is commonly used as an alternative constructor. A static method receives no implicit first argument — it cannot access class or instance data. It is just a utility function grouped with the class for logical organization.

**Q: What is `super()` used for?**
> `super()` gives access to the parent class's methods and constructor. In a child class's `__init__`, `super().__init__()` calls the parent constructor so parent attributes are properly initialized. In overridden methods, `super().method()` calls the parent's version, allowing you to extend behavior rather than replace it entirely.

**Q: What is method overriding vs method overloading?**
> Method overriding is when a child class provides its own implementation of a method defined in the parent class — same name, same parameters. Python supports this fully. Method overloading is defining multiple methods with the same name but different parameters — Python does NOT support this directly. The last defined version wins. Instead, use default parameters or `*args` to handle multiple signatures.

**Q: What is MRO in Python?**
> MRO stands for Method Resolution Order — the order in which Python searches classes when looking up a method in multiple inheritance. Python uses the C3 linearization algorithm — it searches left to right and depth first. You can check it with `ClassName.__mro__`. This determines which parent's method gets called when multiple parents define the same method.

**Q: What is the difference between `__str__` and `__repr__`?**
> `__str__` returns a human-readable string representation — called by `print()` and `str()`. It should be informative for end users. `__repr__` returns a developer-oriented string — called by `repr()` and shown in the REPL. It should ideally be a string that could recreate the object. If only `__repr__` is defined, Python uses it as a fallback for `__str__` too.
