# OOP in Python — Inheritance
> OOP Series | File 04 of 08 | Interview Ready

---

## 1. What is Inheritance?

Inheritance allows a class (child/subclass) to **acquire the attributes and methods of another class (parent/superclass)** — reusing and extending existing code without rewriting it.

```
Without Inheritance:
  class Dog:   class Cat:   class Bird:
    name         name         name
    age          age          age
    eat()        eat()        eat()
    sleep()      sleep()      sleep()
    bark()       meow()       fly()
  → Duplicate code everywhere

With Inheritance:
  class Animal:          ← parent (common code lives here)
    name, age, eat(), sleep()

  class Dog(Animal):     ← child (only unique code)
    bark()
  class Cat(Animal):
    meow()
  class Bird(Animal):
    fly()
```

**Key terms:**
| Term | Meaning |
|---|---|
| Parent / Base / Super class | The class being inherited from |
| Child / Derived / Sub class | The class that inherits |
| `super()` | Refers to the parent class |
| `is-a` relationship | Dog **is-a** Animal — the inheritance test |

---

## 2. Basic Inheritance Syntax

```python
class Animal:                           # Parent class
    def __init__(self, name, age):
        self.name = name
        self.age  = age

    def eat(self):
        print(f"{self.name} is eating")

    def sleep(self):
        print(f"{self.name} is sleeping")

    def __str__(self):
        return f"{self.__class__.__name__}(name={self.name}, age={self.age})"


class Dog(Animal):                      # Child class — inherits Animal
    def __init__(self, name, age, breed):
        super().__init__(name, age)     # call parent __init__
        self.breed = breed

    def bark(self):                     # Dog-specific method
        print(f"{self.name} says: Woof!")


class Cat(Animal):                      # Another child of Animal
    def __init__(self, name, age, indoor):
        super().__init__(name, age)
        self.indoor = indoor

    def meow(self):
        print(f"{self.name} says: Meow!")


# Usage
dog = Dog("Bruno", 3, "Labrador")
cat = Cat("Whiskers", 2, True)

dog.eat()           # Bruno is eating    ← inherited from Animal
dog.sleep()         # Bruno is sleeping  ← inherited from Animal
dog.bark()          # Bruno says: Woof!  ← Dog's own method

cat.eat()           # Whiskers is eating ← inherited
cat.meow()          # Whiskers says: Meow!

print(dog)          # Dog(name=Bruno, age=3)   ← __str__ from Animal

# isinstance checks
print(isinstance(dog, Dog))      # True
print(isinstance(dog, Animal))   # True  ← dog IS-A Animal
print(isinstance(cat, Dog))      # False
```

---

## 3. `super()` — Calling Parent Methods

`super()` gives you access to the parent class. Most commonly used in `__init__` to avoid duplicating initialization code.

```python
class Vehicle:
    def __init__(self, brand, speed):
        self.brand = brand
        self.speed = speed
        print(f"Vehicle.__init__ called: {brand}")

    def describe(self):
        print(f"{self.brand} — max speed: {self.speed} km/h")


class Car(Vehicle):
    def __init__(self, brand, speed, doors):
        super().__init__(brand, speed)       # ← calls Vehicle.__init__
        self.doors = doors
        print(f"Car.__init__ called: {doors} doors")

    def describe(self):
        super().describe()                   # ← calls Vehicle.describe
        print(f"Doors: {self.doors}")


class ElectricCar(Car):
    def __init__(self, brand, speed, doors, battery):
        super().__init__(brand, speed, doors)  # ← calls Car.__init__
        self.battery = battery

    def describe(self):
        super().describe()                   # ← calls Car.describe
        print(f"Battery: {self.battery} kWh")


ec = ElectricCar("Tesla", 250, 4, 100)
# Output:
# Vehicle.__init__ called: Tesla
# Car.__init__ called: 4 doors

print()
ec.describe()
# Output:
# Tesla — max speed: 250 km/h
# Doors: 4
# Battery: 100 kWh
```

> **Important:** Always call `super().__init__()` in the child's `__init__` when the parent has one — otherwise the parent's attributes won't be set up.

---

## 4. Types of Inheritance

### 4a. Single Inheritance
One child, one parent. Most common.

```python
class Animal:
    def breathe(self): print("Breathing")

class Dog(Animal):
    def bark(self): print("Woof!")

d = Dog()
d.breathe()   # Breathing
d.bark()      # Woof!
```

---

### 4b. Multilevel Inheritance
A chain: child becomes parent of another child.

```python
class Animal:
    def eat(self):
        print("Eating")

class Mammal(Animal):              # Mammal inherits Animal
    def breathe(self):
        print("Breathing with lungs")

class Dog(Mammal):                 # Dog inherits Mammal (which inherits Animal)
    def bark(self):
        print("Woof!")

d = Dog()
d.eat()       # Eating      ← from Animal (2 levels up)
d.breathe()   # Breathing with lungs  ← from Mammal
d.bark()      # Woof!       ← from Dog

print(Dog.__mro__)
# (<class 'Dog'>, <class 'Mammal'>, <class 'Animal'>, <class 'object'>)
```

---

### 4c. Multiple Inheritance
One child inherits from two or more parents.

```python
class Flyable:
    def fly(self):
        print("Flying")

class Swimmable:
    def swim(self):
        print("Swimming")

class Duck(Flyable, Swimmable):    # inherits BOTH
    def quack(self):
        print("Quack!")

d = Duck()
d.fly()     # Flying
d.swim()    # Swimming
d.quack()   # Quack!
```

---

### 4d. Hierarchical Inheritance
One parent, multiple children.

```python
class Shape:
    def area(self): pass
    def describe(self): print(f"I am a {self.__class__.__name__}")

class Circle(Shape):
    def __init__(self, r): self.r = r
    def area(self): return 3.14 * self.r ** 2

class Rectangle(Shape):
    def __init__(self, w, h): self.w = w; self.h = h
    def area(self): return self.w * self.h

class Triangle(Shape):
    def __init__(self, b, h): self.b = b; self.h = h
    def area(self): return 0.5 * self.b * self.h

shapes = [Circle(5), Rectangle(4, 6), Triangle(3, 8)]
for s in shapes:
    s.describe()
    print(f"  Area: {s.area()}")
# I am a Circle      Area: 78.5
# I am a Rectangle   Area: 24
# I am a Triangle    Area: 12.0
```

---

### 4e. Hybrid Inheritance
Combination of two or more types. Python uses **MRO** to resolve method lookup order (see Section 6).

---

## 5. Method Overriding

A child class can **redefine** a method inherited from the parent. Python always calls the child's version first.

```python
class Animal:
    def sound(self):
        print("Some animal sound")

    def describe(self):
        self.sound()         # calls the overridden version (dynamic dispatch)
        print(f"I am {self.name}")


class Dog(Animal):
    def __init__(self, name):
        self.name = name

    def sound(self):         # overrides Animal.sound
        print("Woof!")


class Cat(Animal):
    def __init__(self, name):
        self.name = name

    def sound(self):         # overrides Animal.sound
        print("Meow!")


animals = [Dog("Bruno"), Cat("Whiskers")]
for a in animals:
    a.describe()
# Woof!      I am Bruno
# Meow!      I am Whiskers
```

**Calling parent version alongside override:**
```python
class Employee:
    def __init__(self, name, salary):
        self.name   = name
        self.salary = salary

    def details(self):
        print(f"Name: {self.name}, Salary: ₹{self.salary}")


class Manager(Employee):
    def __init__(self, name, salary, team_size):
        super().__init__(name, salary)
        self.team_size = team_size

    def details(self):              # override — but also call parent
        super().details()           # ← reuse parent's output
        print(f"Team Size: {self.team_size}")


m = Manager("AJ", 90000, 8)
m.details()
# Name: AJ, Salary: ₹90000
# Team Size: 8
```

---

## 6. MRO — Method Resolution Order

When a method is called, Python looks through the class hierarchy in a specific order using the **C3 Linearization algorithm**. This matters most in multiple inheritance.

```python
class A:
    def hello(self): print("Hello from A")

class B(A):
    def hello(self): print("Hello from B")

class C(A):
    def hello(self): print("Hello from C")

class D(B, C):       # multiple inheritance
    pass

d = D()
d.hello()            # Hello from B  ← Python followed MRO

print(D.__mro__)
# (<class 'D'>, <class 'B'>, <class 'C'>, <class 'A'>, <class 'object'>)

# Or more readable:
print([cls.__name__ for cls in D.__mro__])
# ['D', 'B', 'C', 'A', 'object']
```

**MRO rule (simplified):** Python looks left to right across parent classes, then goes up. D → B → C → A → object. This is called the **Diamond Problem** solution.

```
        A
       / \
      B   C
       \ /
        D
```

```python
# Practical MRO with super() chain
class A:
    def method(self):
        print("A")

class B(A):
    def method(self):
        print("B")
        super().method()

class C(A):
    def method(self):
        print("C")
        super().method()

class D(B, C):
    def method(self):
        print("D")
        super().method()

D().method()
# D → B → C → A
# (super() in each class follows MRO, not just immediate parent)
```

---

## 7. `isinstance()` and `issubclass()`

```python
class Animal: pass
class Dog(Animal): pass
class Cat(Animal): pass
class GoldenRetriever(Dog): pass

g = GoldenRetriever()

print(isinstance(g, GoldenRetriever))   # True
print(isinstance(g, Dog))               # True  — walks up hierarchy
print(isinstance(g, Animal))            # True
print(isinstance(g, Cat))               # False

print(issubclass(GoldenRetriever, Dog))     # True
print(issubclass(GoldenRetriever, Animal))  # True
print(issubclass(Dog, Cat))                 # False
print(issubclass(Dog, Dog))                 # True — a class is subclass of itself
```

---

## 8. Inheritance with `__slots__`

```python
class Animal:
    __slots__ = ["name", "age"]

    def __init__(self, name, age):
        self.name = name
        self.age  = age

class Dog(Animal):
    __slots__ = ["breed"]          # adds breed; name and age come from Animal

    def __init__(self, name, age, breed):
        super().__init__(name, age)
        self.breed = breed

d = Dog("Bruno", 3, "Labrador")
print(d.name, d.age, d.breed)     # Bruno 3 Labrador
# d.color = "Brown"               # ❌ AttributeError — slots restrict this
```

---

## 9. Abstract Base Class Preview

Sometimes a parent class should **not** be instantiated — it only exists to define a structure for children. Use `ABC` and `@abstractmethod` for this (covered fully in File 06 — Abstraction).

```python
from abc import ABC, abstractmethod

class Shape(ABC):
    @abstractmethod
    def area(self):       # subclasses MUST implement this
        pass

    @abstractmethod
    def perimeter(self):
        pass

    def describe(self):   # concrete method — subclasses can use as-is
        print(f"Area: {self.area():.2f}, Perimeter: {self.perimeter():.2f}")


class Circle(Shape):
    def __init__(self, r):
        self.r = r

    def area(self):
        return 3.14159 * self.r ** 2

    def perimeter(self):
        return 2 * 3.14159 * self.r


# shape = Shape()   # ❌ TypeError: Can't instantiate abstract class
c = Circle(5)
c.describe()         # Area: 78.54, Perimeter: 31.42
```

---

## 10. DSA Pattern — Linked List with Inheritance

```python
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

class LinkedList:
    def __init__(self):
        self.head = None

    def append(self, data):
        new_node = Node(data)
        if not self.head:
            self.head = new_node
            return
        curr = self.head
        while curr.next:
            curr = curr.next
        curr.next = new_node

    def display(self):
        result = []
        curr = self.head
        while curr:
            result.append(str(curr.data))
            curr = curr.next
        print(" → ".join(result))

class SortedLinkedList(LinkedList):         # inherits LinkedList
    def append(self, data):                 # overrides append — inserts sorted
        new_node = Node(data)
        if not self.head or data < self.head.data:
            new_node.next = self.head
            self.head = new_node
            return
        curr = self.head
        while curr.next and curr.next.data < data:
            curr = curr.next
        new_node.next = curr.next
        curr.next = new_node


sll = SortedLinkedList()
sll.append(5)
sll.append(2)
sll.append(8)
sll.append(1)
sll.display()     # 1 → 2 → 5 → 8   ← sorted automatically
```

---

## Quick Reference

```python
# BASIC INHERITANCE
class Child(Parent):
    def __init__(self, ...):
        super().__init__(...)    # always call parent init

# MULTIPLE INHERITANCE
class Child(Parent1, Parent2):
    pass

# MRO
print(ClassName.__mro__)         # full MRO tuple
print(ClassName.mro())           # same as list

# TYPES
# Single:       Child(Parent)
# Multilevel:   C(B) → B(A)
# Multiple:     D(B, C)
# Hierarchical: B(A), C(A)

# CHECKS
isinstance(obj, ClassName)       # True if obj is instance of class or its parent
issubclass(Child, Parent)        # True if Child inherits from Parent
```

---

## Interview Short Answers

**Q: What is inheritance and what problem does it solve?**
> Inheritance lets a child class acquire attributes and methods from a parent class without rewriting them. It solves code duplication — common behavior lives in one parent class and all children reuse it. It also models real-world "is-a" relationships: a Dog is-a Animal, a Manager is-an Employee. This makes the code easier to maintain — a change in the parent propagates to all children automatically.

**Q: What is the difference between `super().__init__()` and `ParentClass.__init__(self)`?**
> Both call the parent's `__init__`, but `super()` is the preferred way. `super()` is dynamic — it follows the MRO, so in multiple inheritance it calls the correct next class in the chain. Calling `ParentClass.__init__(self)` hardcodes the parent name, which breaks the cooperative multiple inheritance pattern and causes issues if the class hierarchy changes.

**Q: What is the Diamond Problem and how does Python solve it?**
> The Diamond Problem occurs in multiple inheritance when two parent classes share a common ancestor. For example, D inherits from B and C, both of which inherit from A. When `D.method()` is called, which version of `A.method()` should run, via B or via C? Python solves this with the MRO (Method Resolution Order) using C3 Linearization — it creates a consistent, predictable order: D → B → C → A. `super()` in each class follows this order rather than jumping straight to the immediate parent.

**Q: What is method overriding? When would you use it?**
> Method overriding is when a child class defines a method with the same name as a parent class method. Python always calls the child's version. You use it when the child needs specialized behavior — a Dog's `sound()` says "Woof" while the parent Animal's `sound()` says "Generic sound". You can still call the parent's version inside the override using `super().method()` to extend rather than completely replace the behavior.

**Q: What is MRO?**
> Method Resolution Order is the sequence Python follows when looking up a method or attribute in an inheritance hierarchy. Python uses the C3 Linearization algorithm to compute this order, which ensures that each class in the hierarchy appears exactly once and maintains left-to-right order among siblings. It is accessible as `ClassName.__mro__` or `ClassName.mro()`. It matters most in multiple inheritance — `super()` follows MRO, not just the immediate parent.

**Q: What is the difference between multilevel and multiple inheritance?**
> Multilevel inheritance is a chain: class C inherits from B which inherits from A. It represents a specialization hierarchy — Animal → Mammal → Dog. Multiple inheritance is when one class inherits from two or more unrelated parents simultaneously — class Duck inherits from both Flyable and Swimmable. Multiple inheritance is more powerful but needs careful design to avoid the Diamond Problem; Python handles it via MRO.

**Q: What is `isinstance()` and why is it better than `type() ==`?**
> `isinstance(obj, ClassName)` returns True if the object is an instance of that class or any of its parent classes. `type(obj) == ClassName` only returns True for the exact class — it fails for subclass instances. For example, `isinstance(dog, Animal)` returns True because Dog is a subclass of Animal, but `type(dog) == Animal` returns False. `isinstance` is more flexible and is the idiomatic Python way to check object types in inheritance hierarchies.
