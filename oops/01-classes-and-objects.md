# OOP in Python — Classes and Objects
> OOP Series | File 01 of 08 | Interview Ready

---

## 1. What is Object-Oriented Programming?

Object-Oriented Programming (OOP) is a programming paradigm that organizes code around **objects** rather than functions and logic alone.

```
Procedural Programming  → code is a sequence of instructions
Object-Oriented         → code is a collection of objects that interact
```

**Real-world analogy:**
```
Class  → blueprint of a Car (design on paper)
Object → actual Car built from that blueprint (exists in reality)

One blueprint → many cars
One class     → many objects
```

**Why OOP?**
- Models real-world entities naturally
- Code is reusable — write once, use in many objects
- Code is modular — each class handles its own responsibility
- Easier to maintain and scale large projects
- Reduces code repetition (DRY — Don't Repeat Yourself)

---

## 2. What is a Class?

A **class** is a user-defined blueprint or template that defines:
- **Attributes** — data the object holds (variables)
- **Methods** — actions the object can perform (functions)

### Syntax
```python
class ClassName:
    # attributes and methods go here
    pass
```

### Rules for class names
- Use **PascalCase** (CapitalizeEachWord) — `Student`, `BankAccount`, `LinkedList`
- Should be a noun — it represents a thing
- No spaces or hyphens

```python
# Correct
class Student:
    pass

class BankAccount:
    pass

class LinkedList:
    pass

# Wrong
class student: pass       # ❌ should be PascalCase
class bank_account: pass  # ❌ use PascalCase not snake_case
```

---

## 3. What is an Object?

An **object** is a specific instance created from a class. Each object:
- Has its own copy of the class attributes
- Can call the class methods
- Exists independently in memory

```python
class Student:
    pass

# Creating objects (instances)
s1 = Student()   # s1 is an object of Student class
s2 = Student()   # s2 is a different object of same class

print(type(s1))           # Output: <class '__main__.Student'>
print(type(s2))           # Output: <class '__main__.Student'>

print(id(s1))             # memory address of s1
print(id(s2))             # different memory address

print(s1 == s2)           # Output: False — different objects
print(s1 is s2)           # Output: False — not same object in memory
```

**Memory model:**
```
s1 ──► [ Student object ] at address 0x1234
s2 ──► [ Student object ] at address 0x5678

Same class, different objects, different memory locations
```

---

## 4. `__init__` — Constructor

`__init__` is a special method called automatically when an object is created. It **initializes** the object's attributes.

```python
class Student:
    def __init__(self, name, age, marks):
        self.name  = name     # initialize instance attributes
        self.age   = age
        self.marks = marks

# Creating objects — __init__ is called automatically
s1 = Student("AJ", 22, 85)
s2 = Student("Rahul", 21, 92)

print(s1.name)    # Output: AJ
print(s1.age)     # Output: 22
print(s2.marks)   # Output: 92
```

**What `self` means:**
```python
s1 = Student("AJ", 22, 85)

# Python internally does this:
# Student.__init__(s1, "AJ", 22, 85)
# self = s1
# self.name = "AJ"  →  s1.name = "AJ"
```

> **`self` is not a keyword** — it is just a naming convention. You could name it anything, but `self` is universally used and expected in interviews.

```python
# This works but never do it
class Student:
    def __init__(this, name):   # 'this' works but wrong convention
        this.name = name
```

---

## 5. Instance Attributes vs Class Attributes

### Instance Attributes
- Defined inside `__init__` using `self`
- **Unique to each object** — each object has its own copy
- Accessed via `object.attribute`

```python
class Student:
    def __init__(self, name, marks):
        self.name  = name    # instance attribute
        self.marks = marks   # instance attribute

s1 = Student("AJ", 85)
s2 = Student("Rahul", 92)

# Each object has its own values
print(s1.name)   # AJ
print(s2.name)   # Rahul   ← different from s1

# Modify one object — doesn't affect the other
s1.marks = 95
print(s1.marks)  # 95
print(s2.marks)  # 92  ← unchanged
```

### Class Attributes
- Defined directly inside the class body (outside `__init__`)
- **Shared by ALL objects** of that class
- Accessed via `ClassName.attribute` or `object.attribute`

```python
class Student:
    school  = "VTU"       # class attribute — shared
    count   = 0           # tracks total students created

    def __init__(self, name, marks):
        self.name  = name   # instance attribute
        self.marks = marks
        Student.count += 1  # update class attribute

s1 = Student("AJ", 85)
s2 = Student("Rahul", 92)
s3 = Student("Priya", 78)

print(s1.school)        # Output: VTU
print(s2.school)        # Output: VTU  — same value
print(Student.school)   # Output: VTU  — access via class name
print(Student.count)    # Output: 3    — all 3 students counted
```

### ⚠️ The Shadowing Gotcha
```python
class Student:
    school = "VTU"

s1 = Student()
s2 = Student()

# Changing via class — affects ALL objects
Student.school = "MIT"
print(s1.school)   # MIT
print(s2.school)   # MIT

# Setting on INSTANCE — creates instance attribute, shadows class attribute
s1.school = "IIT"           # creates s1's own 'school' attribute
print(s1.school)   # IIT   ← s1's own instance attribute
print(s2.school)   # MIT   ← still the class attribute
print(Student.school)  # MIT ← class attribute unchanged
```

---

## 6. Instance Methods

Methods are functions defined inside a class. They always take `self` as the first parameter.

```python
class Student:
    def __init__(self, name, marks):
        self.name  = name
        self.marks = marks

    def display(self):                    # method with no extra params
        print(f"Name: {self.name}, Marks: {self.marks}")

    def grade(self):                      # method that returns a value
        if self.marks >= 90:
            return "A"
        elif self.marks >= 75:
            return "B"
        elif self.marks >= 60:
            return "C"
        else:
            return "F"

    def update_marks(self, new_marks):    # method with parameter
        old = self.marks
        self.marks = new_marks
        print(f"Marks updated: {old} → {self.marks}")

    def is_passed(self):
        return self.marks >= 40

s1 = Student("AJ", 85)
s1.display()                   # Output: Name: AJ, Marks: 85
print(s1.grade())              # Output: B
print(s1.is_passed())          # Output: True

s1.update_marks(95)            # Output: Marks updated: 85 → 95
print(s1.grade())              # Output: A
```

---

## 7. `__dict__` — Inspecting Object Attributes

`__dict__` returns a dictionary of all attributes of an object or class.

```python
class Student:
    school = "VTU"

    def __init__(self, name, age, marks):
        self.name  = name
        self.age   = age
        self.marks = marks

s1 = Student("AJ", 22, 85)

# Instance __dict__ — only instance attributes
print(s1.__dict__)
# Output: {'name': 'AJ', 'age': 22, 'marks': 85}

# Class __dict__ — class attributes + methods
print(Student.__dict__)
# Output: {'school': 'VTU', '__init__': <function...>, ...}

# Dynamically add attribute
s1.city = "Bengaluru"
print(s1.__dict__)
# Output: {'name': 'AJ', 'age': 22, 'marks': 85, 'city': 'Bengaluru'}

# Access attribute by name as string
attr = "name"
print(s1.__dict__[attr])   # Output: AJ

# Using getattr() — same as above but cleaner
print(getattr(s1, "name"))         # Output: AJ
print(getattr(s1, "gpa", "N/A"))   # Output: N/A (default if not found)

# Using setattr()
setattr(s1, "marks", 99)
print(s1.marks)   # Output: 99

# Using hasattr()
print(hasattr(s1, "name"))    # Output: True
print(hasattr(s1, "salary"))  # Output: False

# Using delattr()
delattr(s1, "city")
print(s1.__dict__)   # city is gone
```

---

## 8. Built-in Class Attributes

Every class in Python has built-in attributes automatically.

```python
class Student:
    """This class represents a student."""

    school = "VTU"

    def __init__(self, name):
        self.name = name

    def display(self):
        print(self.name)

# __name__ — name of the class as string
print(Student.__name__)      # Output: Student

# __doc__ — docstring of the class
print(Student.__doc__)       # Output: This class represents a student.

# __module__ — module where the class is defined
print(Student.__module__)    # Output: __main__

# __bases__ — tuple of parent classes
print(Student.__bases__)     # Output: (<class 'object'>,)

# __dict__ — all class attributes and methods
print(Student.__dict__)

# Every class implicitly inherits from object
print(isinstance(Student(), object))   # Output: True
```

---

## 9. `del` — Deleting Objects and Attributes

```python
class Student:
    def __init__(self, name, marks):
        self.name  = name
        self.marks = marks

s1 = Student("AJ", 85)
s2 = Student("Rahul", 92)

# Delete an attribute from an object
del s1.marks
print(s1.__dict__)   # Output: {'name': 'AJ'}  — marks is gone
# print(s1.marks)    # ❌ AttributeError

# Delete an object entirely
del s2
# print(s2.name)     # ❌ NameError: s2 is not defined
```

```python
# __del__ — called when object is about to be garbage collected
class Student:
    def __init__(self, name):
        self.name = name

    def __del__(self):
        print(f"{self.name} object deleted from memory")

s1 = Student("AJ")
del s1
# Output: AJ object deleted from memory
```

---

## 10. `isinstance()` and `issubclass()`

```python
class Animal:
    pass

class Dog(Animal):
    pass

class Cat(Animal):
    pass

d = Dog()
c = Cat()

# isinstance — check if object is instance of a class
print(isinstance(d, Dog))     # True
print(isinstance(d, Animal))  # True  — Dog IS an Animal (inheritance)
print(isinstance(d, Cat))     # False

# isinstance with multiple types — tuple
print(isinstance(d, (Dog, Cat)))   # True — is it a Dog OR a Cat?

# issubclass — check class relationship
print(issubclass(Dog, Animal))  # True
print(issubclass(Cat, Dog))     # False
print(issubclass(Dog, object))  # True — everything inherits from object

# type() vs isinstance()
print(type(d) == Dog)     # True — exact type only
print(type(d) == Animal)  # False — doesn't consider inheritance

# isinstance() is preferred in interviews — respects inheritance
```

> **Interview tip:** Always use `isinstance()` over `type() ==` for type checking — `isinstance()` respects the inheritance chain while `type()` checks exact type only.

---

## 11. Dynamic Attributes

Python allows adding attributes to objects at runtime — not just inside `__init__`.

```python
class Student:
    def __init__(self, name):
        self.name = name

s1 = Student("AJ")

# Add attribute dynamically
s1.marks = 85
s1.city  = "Bengaluru"
s1.grade = "A"

print(s1.__dict__)
# {'name': 'AJ', 'marks': 85, 'city': 'Bengaluru', 'grade': 'A'}

# Different objects can have different attributes
s2 = Student("Rahul")
s2.marks = 92
# s2 does not have city or grade — that's fine in Python

print(s2.__dict__)   # {'name': 'Rahul', 'marks': 92}
```

> **Interview tip:** Python is dynamically typed and allows this. But in real projects, always define all attributes in `__init__` for clarity and consistency. Use `__slots__` to restrict dynamic attributes (covered in File 03 — Encapsulation).

---

## 12. Object Comparison

By default Python compares objects by **identity** (memory address), not value.

```python
class Student:
    def __init__(self, name, marks):
        self.name  = name
        self.marks = marks

s1 = Student("AJ", 85)
s2 = Student("AJ", 85)   # same values, different object

print(s1 == s2)    # Output: False  ← compares by identity by default
print(s1 is s2)    # Output: False  ← different objects in memory

# To compare by value — override __eq__
class Student:
    def __init__(self, name, marks):
        self.name  = name
        self.marks = marks

    def __eq__(self, other):
        return self.name == other.name and self.marks == other.marks

s1 = Student("AJ", 85)
s2 = Student("AJ", 85)

print(s1 == s2)    # Output: True  ← now compares by value
print(s1 is s2)    # Output: False ← still different objects in memory
```

---

## Quick Reference

```python
# DEFINE A CLASS
class ClassName:
    class_attr = value          # class attribute — shared

    def __init__(self, params): # constructor — called on object creation
        self.attr = value       # instance attribute — unique per object

    def method(self):           # instance method
        pass

# CREATE OBJECTS
obj = ClassName(args)

# ACCESS
obj.attr                        # instance attribute
ClassName.class_attr            # class attribute (preferred)
obj.class_attr                  # also works

# INSPECT
obj.__dict__                    # all instance attributes as dict
ClassName.__name__              # class name as string
ClassName.__doc__               # docstring
ClassName.__bases__             # parent classes

# DYNAMIC ATTRIBUTE OPERATIONS
getattr(obj, "attr")            # get attribute by name string
getattr(obj, "attr", default)   # with default if not found
setattr(obj, "attr", value)     # set attribute by name string
hasattr(obj, "attr")            # check if attribute exists
delattr(obj, "attr")            # delete attribute

# TYPE CHECKING
type(obj)                       # exact type
isinstance(obj, Class)          # is obj an instance? (respects inheritance)
isinstance(obj, (A, B))         # is obj A or B?
issubclass(Child, Parent)       # class relationship check

# DELETE
del obj.attr                    # delete attribute
del obj                         # delete object
```

---

## Interview Short Answers

**Q: What is the difference between a class and an object?**
> A class is a blueprint or template that defines attributes and methods. An object is a specific instance created from that blueprint — it exists in memory and has its own data. For example, `Student` is a class and `s1 = Student("AJ", 85)` creates an object. You can create many objects from one class, each with different data but sharing the same structure and behavior.

**Q: What is `self` in Python?**
> `self` refers to the current instance of the class — the specific object calling the method. It is always the first parameter of instance methods. Python passes it automatically; you never pass it manually when calling. Through `self`, each object accesses its own attributes and methods, keeping them separate from other objects of the same class.

**Q: What is the difference between instance attributes and class attributes?**
> Instance attributes are defined inside `__init__` using `self` and belong to each individual object — each object has its own independent copy. Class attributes are defined directly in the class body and are shared by all objects. Accessing a class attribute through an object works, but modifying it through an object creates a new instance attribute that shadows the class attribute for that object only — the class attribute remains unchanged.

**Q: What is `__dict__` in Python?**
> `__dict__` is a built-in attribute available on every object and class. For an object, it returns a dictionary of all instance attributes and their values. For a class, it returns all class attributes and methods. It is useful for inspecting and dynamically accessing attributes. The built-in functions `getattr()`, `setattr()`, `hasattr()`, and `delattr()` provide a cleaner way to work with attributes dynamically.

**Q: What is the difference between `type()` and `isinstance()`?**
> `type(obj) == Class` checks the exact type only — it returns False if `obj` is an instance of a subclass. `isinstance(obj, Class)` checks if `obj` is an instance of `Class` or any subclass of it — it respects the inheritance chain. `isinstance()` is preferred in professional code and interviews because it supports polymorphism correctly.

**Q: What are built-in class attributes in Python?**
> Every Python class has built-in attributes automatically. `__name__` is the class name as a string. `__doc__` is the docstring. `__module__` is the module where the class is defined. `__bases__` is a tuple of direct parent classes. `__dict__` contains all class attributes and methods. All classes in Python implicitly inherit from `object`, which provides these attributes through the inheritance chain.

**Q: Can you add attributes to an object outside `__init__`?**
> Yes — Python allows adding attributes to objects dynamically at runtime, even after creation. You can set them directly (`obj.new_attr = value`) or use `setattr()`. However, in practice, all attributes should be defined in `__init__` for clarity and consistency. If you want to restrict dynamic attributes and save memory, use `__slots__` — it limits which attributes an object can have and prevents dynamic addition.
