# OOP in Python — Abstraction
> OOP Series | File 06 of 08 | Interview Ready

---

## 1. What is Abstraction?

Abstraction means **hiding complex implementation details and exposing only what is necessary**. You show the "what" and hide the "how".

```
Without Abstraction:
  User must know HOW everything works internally
  → Complicated, tightly coupled, hard to maintain

With Abstraction:
  User only knows WHAT operations are available
  → Simple interface, implementation can change freely
```

**Real-world analogy:**
```
Car Dashboard:
  You see:  Steering wheel, accelerator, brake, gear
  Hidden:   Engine combustion, transmission, ABS logic, fuel injection

You drive the car without knowing how the engine works.
That is abstraction.
```

**Two levels of abstraction in Python:**
1. **Abstract Classes** — via `abc` module (`ABC` + `@abstractmethod`)
2. **Interfaces** — Python has no `interface` keyword; abstract classes serve this role

---

## 2. The `abc` Module

Python's `abc` (Abstract Base Classes) module provides tools to define abstract classes.

```python
from abc import ABC, abstractmethod

class Animal(ABC):             # Abstract class — cannot be instantiated
    @abstractmethod
    def sound(self):           # Abstract method — MUST be implemented by subclass
        pass

    @abstractmethod
    def move(self):
        pass

    def breathe(self):         # Concrete method — has implementation, inherited as-is
        print("Breathing...")

# a = Animal()   # ❌ TypeError: Can't instantiate abstract class Animal
#                   with abstract methods move, sound
```

**Key rules:**
| Rule | Detail |
|---|---|
| Abstract class | Inherits from `ABC` |
| Abstract method | Decorated with `@abstractmethod` |
| Cannot instantiate | Calling `Animal()` raises `TypeError` |
| Subclass must implement ALL abstract methods | Or it also becomes abstract |
| Concrete methods are inherited normally | No need to override |

---

## 3. Basic Abstract Class

```python
from abc import ABC, abstractmethod

class Shape(ABC):
    @abstractmethod
    def area(self):
        pass

    @abstractmethod
    def perimeter(self):
        pass

    def describe(self):                        # concrete — shared by all shapes
        print(f"{self.__class__.__name__}:")
        print(f"  Area      = {self.area():.2f}")
        print(f"  Perimeter = {self.perimeter():.2f}")


class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius

    def area(self):                            # implements abstract method
        return 3.14159 * self.radius ** 2

    def perimeter(self):
        return 2 * 3.14159 * self.radius


class Rectangle(Shape):
    def __init__(self, width, height):
        self.width  = width
        self.height = height

    def area(self):
        return self.width * self.height

    def perimeter(self):
        return 2 * (self.width + self.height)


class Triangle(Shape):
    def __init__(self, a, b, c):
        self.a = a
        self.b = b
        self.c = c

    def area(self):
        s = (self.a + self.b + self.c) / 2    # Heron's formula
        return (s * (s-self.a) * (s-self.b) * (s-self.c)) ** 0.5

    def perimeter(self):
        return self.a + self.b + self.c


shapes = [Circle(7), Rectangle(4, 6), Triangle(3, 4, 5)]
for shape in shapes:
    shape.describe()
    print()

# Circle:
#   Area      = 153.94
#   Perimeter = 43.98
#
# Rectangle:
#   Area      = 24.00
#   Perimeter = 20.00
#
# Triangle:
#   Area      = 6.00
#   Perimeter = 12.00
```

---

## 4. Partial Implementation — Chained Abstraction

A subclass that doesn't implement all abstract methods is itself abstract.

```python
from abc import ABC, abstractmethod

class Vehicle(ABC):
    @abstractmethod
    def start_engine(self):
        pass

    @abstractmethod
    def stop_engine(self):
        pass

    @abstractmethod
    def fuel_type(self):
        pass


class MotorVehicle(Vehicle):              # still abstract — doesn't implement fuel_type
    def start_engine(self):
        print("Engine started")

    def stop_engine(self):
        print("Engine stopped")

    # fuel_type() still abstract — MotorVehicle cannot be instantiated


class PetrolCar(MotorVehicle):            # concrete — implements remaining method
    def fuel_type(self):
        return "Petrol"


class ElectricCar(MotorVehicle):
    def start_engine(self):               # can override concrete methods too
        print("Electric motor activated (silent)")

    def stop_engine(self):
        print("Electric motor deactivated")

    def fuel_type(self):
        return "Electric"


# mv = MotorVehicle()   # ❌ TypeError — still abstract
pc = PetrolCar()
ec = ElectricCar()

pc.start_engine()          # Engine started
print(pc.fuel_type())      # Petrol

ec.start_engine()          # Electric motor activated (silent)
print(ec.fuel_type())      # Electric
```

---

## 5. Abstract Properties

You can make a property abstract — subclasses must implement the property getter.

```python
from abc import ABC, abstractmethod

class DatabaseConnection(ABC):

    @property
    @abstractmethod
    def connection_string(self):           # abstract property
        pass

    @abstractmethod
    def connect(self):
        pass

    @abstractmethod
    def disconnect(self):
        pass

    def execute(self, query):              # concrete method
        print(f"[{self.__class__.__name__}] Executing: {query}")


class MySQLConnection(DatabaseConnection):
    def __init__(self, host, db):
        self._host = host
        self._db   = db

    @property
    def connection_string(self):           # implements abstract property
        return f"mysql://{self._host}/{self._db}"

    def connect(self):
        print(f"Connected to MySQL at {self.connection_string}")

    def disconnect(self):
        print("MySQL connection closed")


class PostgreSQLConnection(DatabaseConnection):
    def __init__(self, host, db, port=5432):
        self._host = host
        self._db   = db
        self._port = port

    @property
    def connection_string(self):
        return f"postgresql://{self._host}:{self._port}/{self._db}"

    def connect(self):
        print(f"Connected to PostgreSQL at {self.connection_string}")

    def disconnect(self):
        print("PostgreSQL connection closed")


# Polymorphic usage — same interface, different DB
def run_query(db: DatabaseConnection, query: str):
    db.connect()
    db.execute(query)
    db.disconnect()

mysql_db = MySQLConnection("localhost", "myapp")
pg_db    = PostgreSQLConnection("prod-server", "analytics")

run_query(mysql_db, "SELECT * FROM users")
print()
run_query(pg_db, "SELECT COUNT(*) FROM events")
```

---

## 6. Abstract Class with `__init__`

Abstract classes CAN have an `__init__` — it runs when a concrete subclass calls `super().__init__()`.

```python
from abc import ABC, abstractmethod

class Employee(ABC):
    def __init__(self, name, employee_id):
        self.name        = name
        self.employee_id = employee_id

    @abstractmethod
    def calculate_salary(self):
        pass

    @abstractmethod
    def get_role(self):
        pass

    def display(self):
        print(f"ID: {self.employee_id} | Name: {self.name} | "
              f"Role: {self.get_role()} | Salary: ₹{self.calculate_salary():,.0f}")


class FullTimeEmployee(Employee):
    def __init__(self, name, employee_id, monthly_salary):
        super().__init__(name, employee_id)        # calls ABC's __init__
        self.monthly_salary = monthly_salary

    def calculate_salary(self):
        return self.monthly_salary

    def get_role(self):
        return "Full-Time"


class ContractEmployee(Employee):
    def __init__(self, name, employee_id, hourly_rate, hours_worked):
        super().__init__(name, employee_id)
        self.hourly_rate  = hourly_rate
        self.hours_worked = hours_worked

    def calculate_salary(self):
        return self.hourly_rate * self.hours_worked

    def get_role(self):
        return "Contract"


class Intern(Employee):
    def __init__(self, name, employee_id, stipend):
        super().__init__(name, employee_id)
        self.stipend = stipend

    def calculate_salary(self):
        return self.stipend

    def get_role(self):
        return "Intern"


employees = [
    FullTimeEmployee("AJ",    "E001", 80000),
    ContractEmployee("Rahul", "C001", 500, 160),
    Intern("Priya",           "I001", 15000),
]

print("--- Payroll Report ---")
for emp in employees:
    emp.display()

# ID: E001 | Name: AJ    | Role: Full-Time | Salary: ₹80,000
# ID: C001 | Name: Rahul | Role: Contract  | Salary: ₹80,000
# ID: I001 | Name: Priya | Role: Intern    | Salary: ₹15,000
```

---

## 7. Interface Pattern (via ABC)

Python has no `interface` keyword. We simulate interfaces with abstract classes where **all methods are abstract** (no concrete methods, no `__init__`).

```python
from abc import ABC, abstractmethod

# "Interface" — all abstract, no state
class Serializable(ABC):
    @abstractmethod
    def to_json(self) -> str:
        pass

    @abstractmethod
    def to_csv(self) -> str:
        pass


class Printable(ABC):
    @abstractmethod
    def print_details(self):
        pass


# A class can implement multiple interfaces
class Product(Serializable, Printable):
    def __init__(self, name, price, qty):
        self.name  = name
        self.price = price
        self.qty   = qty

    def to_json(self):
        import json
        return json.dumps({"name": self.name, "price": self.price, "qty": self.qty})

    def to_csv(self):
        return f"{self.name},{self.price},{self.qty}"

    def print_details(self):
        print(f"Product: {self.name} | ₹{self.price} | Stock: {self.qty}")


p = Product("Laptop", 75000, 10)
p.print_details()
print(p.to_json())
print(p.to_csv())
# Product: Laptop | ₹75000 | Stock: 10
# {"name": "Laptop", "price": 75000, "qty": 10}
# Laptop,75000,10
```

---

## 8. Abstraction vs Encapsulation

Commonly confused in interviews — here's the clear difference:

| Aspect | Abstraction | Encapsulation |
|---|---|---|
| **Purpose** | Hide complexity, show only interface | Hide data, control access |
| **Focus** | WHAT an object does | HOW data is protected |
| **Mechanism** | Abstract classes, `@abstractmethod` | Access modifiers (`_`, `__`), `@property` |
| **Level** | Design level (what methods exist) | Implementation level (how data is stored) |
| **Example** | `Shape.area()` — every shape has area, but each computes it differently | `BankAccount.__balance` — balance exists but can't be accessed directly |
| **Benefit** | Flexible, interchangeable implementations | Data integrity, validation |

```
Abstraction  = "I don't need to know HOW the engine works to drive"
Encapsulation = "I cannot directly touch the engine — only through controlled access"
```

---

## 9. `ABCMeta` — Alternative Syntax

`ABC` is a convenience class. Under the hood it uses `ABCMeta` as its metaclass. You can use either style:

```python
from abc import ABCMeta, abstractmethod

# Style 1: inherit from ABC (recommended, cleaner)
from abc import ABC
class MyClass(ABC):
    @abstractmethod
    def method(self): pass

# Style 2: use metaclass=ABCMeta explicitly (older style)
class MyClass(metaclass=ABCMeta):
    @abstractmethod
    def method(self): pass

# Both are equivalent
```

---

## 10. DSA Pattern — Pluggable Sort Strategy (Strategy Pattern)

Abstraction enables the **Strategy Pattern** — swap algorithms without changing the calling code.

```python
from abc import ABC, abstractmethod

class SortStrategy(ABC):
    @abstractmethod
    def sort(self, data: list) -> list:
        pass


class BubbleSort(SortStrategy):
    def sort(self, data):
        arr = data[:]
        n = len(arr)
        for i in range(n):
            for j in range(n - i - 1):
                if arr[j] > arr[j+1]:
                    arr[j], arr[j+1] = arr[j+1], arr[j]
        return arr


class MergeSort(SortStrategy):
    def sort(self, data):
        if len(data) <= 1:
            return data
        mid   = len(data) // 2
        left  = self.sort(data[:mid])
        right = self.sort(data[mid:])
        return self._merge(left, right)

    def _merge(self, left, right):
        result = []
        i = j  = 0
        while i < len(left) and j < len(right):
            if left[i] <= right[j]:
                result.append(left[i]); i += 1
            else:
                result.append(right[j]); j += 1
        return result + left[i:] + right[j:]


class PythonBuiltinSort(SortStrategy):
    def sort(self, data):
        return sorted(data)


class Sorter:
    def __init__(self, strategy: SortStrategy):
        self._strategy = strategy

    def set_strategy(self, strategy: SortStrategy):   # swap at runtime
        self._strategy = strategy

    def sort(self, data):
        return self._strategy.sort(data)


data = [64, 34, 25, 12, 22, 11, 90]

sorter = Sorter(BubbleSort())
print("Bubble:", sorter.sort(data))

sorter.set_strategy(MergeSort())
print("Merge: ", sorter.sort(data))

sorter.set_strategy(PythonBuiltinSort())
print("Python:", sorter.sort(data))
# All produce: [11, 12, 22, 25, 34, 64, 90]
```

---

## Quick Reference

```python
from abc import ABC, abstractmethod

# ABSTRACT CLASS
class MyABC(ABC):
    @abstractmethod
    def required_method(self):        # subclass MUST implement
        pass

    @property
    @abstractmethod
    def required_property(self):      # subclass MUST implement as property
        pass

    def optional_method(self):        # concrete — subclass inherits as-is
        pass

# CONCRETE SUBCLASS — must implement ALL abstract methods/properties
class Concrete(MyABC):
    def required_method(self):
        return "implemented"

    @property
    def required_property(self):
        return "value"

# CHECK
from abc import ABC
print(issubclass(Concrete, MyABC))    # True
print(isinstance(Concrete(), MyABC))  # True

# CANNOT instantiate abstract class
# MyABC()   # ❌ TypeError
```

---

## Interview Short Answers

**Q: What is abstraction in OOP?**
> Abstraction means hiding implementation details and exposing only the necessary interface. It answers the question "what does this object do?" without revealing "how does it do it?". In Python, abstraction is implemented using the `abc` module — an abstract class defines a contract (which methods must exist) without implementing them. Subclasses fill in the implementation. For example, a `Shape` abstract class says every shape must have `area()` and `perimeter()`, but each shape — Circle, Rectangle, Triangle — implements them differently.

**Q: What is an abstract class? Can it have concrete methods?**
> An abstract class is a class that cannot be instantiated directly — it exists only to be subclassed. It is defined by inheriting from `ABC` and marking at least one method with `@abstractmethod`. Yes, abstract classes can and often should have concrete methods — these are methods with actual implementations that all subclasses inherit and reuse. For example, a `Shape` abstract class might have abstract `area()` and `perimeter()` methods, but a concrete `describe()` method that all shapes share.

**Q: What happens if a subclass doesn't implement all abstract methods?**
> If a subclass inherits from an abstract class but does not implement all abstract methods, the subclass itself becomes abstract and also cannot be instantiated. Python raises a `TypeError` only when you try to instantiate — not at class definition time. This allows building a chain of partial implementations, where intermediate classes add some methods but leave others for further subclasses.

**Q: What is the difference between abstraction and encapsulation?**
> Both hide things, but at different levels. Abstraction hides complexity at the design level — it defines what operations exist (the interface) without exposing how they work internally. The user of a `Shape` doesn't need to know the formula for area. Encapsulation hides data at the implementation level — it restricts direct access to attributes and enforces access through controlled methods. The balance in a `BankAccount` is private; you can only access it through `get_balance()`. Abstraction is about simplifying the interface; encapsulation is about protecting data integrity.

**Q: Does Python have interfaces? How do you simulate them?**
> Python has no `interface` keyword. Interfaces are simulated using abstract classes where every method is abstract — no concrete methods and no instance state. A class can inherit from multiple such abstract classes to implement multiple interfaces. The `Serializable` and `Printable` abstract classes each define a contract; a `Product` class can implement both by inheriting from both and providing all required methods.

**Q: What is `@abstractmethod`? Can it have a body?**
> `@abstractmethod` is a decorator from the `abc` module that marks a method as abstract — meaning any non-abstract subclass must override it, or Python raises a `TypeError` on instantiation. Surprisingly, an abstract method CAN have a body. The body is never called automatically, but subclasses can explicitly call it with `super().method()` to reuse some default logic while still being required to override it. This is useful when there is common base logic but subclasses must customize it.

**Q: What is the Strategy Pattern and how does abstraction enable it?**
> The Strategy Pattern is a design pattern where you define a family of algorithms, put each in its own class, and make them interchangeable at runtime. Abstraction enables this — you define an abstract `SortStrategy` class with an abstract `sort()` method. Concrete classes like `BubbleSort`, `MergeSort`, and `QuickSort` each implement it differently. The calling code only knows the abstract interface and can swap strategies without changing. This is the open/closed principle: open for extension (add new sort), closed for modification (don't change the calling code).
