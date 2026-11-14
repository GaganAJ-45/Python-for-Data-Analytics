# OOP in Python — Encapsulation
> OOP Series | File 03 of 08 | Interview Ready

---

## 1. What is Encapsulation?

Encapsulation is the OOP principle of **bundling data (attributes) and methods together inside a class, and restricting direct access to some of that data**.

```
Without Encapsulation:
  Anyone can read or change any data directly
  → No control, no validation, bugs everywhere

With Encapsulation:
  Data is hidden inside the class
  Access only through controlled methods
  → Validation enforced, data integrity maintained
```

**Real-world analogy:**
```
ATM Machine
  ├── Hidden inside: account balance, PIN, transaction logic
  └── Exposed outside: insert card, enter PIN, withdraw cash

You cannot directly reach in and change the balance.
You can only interact through the controlled interface (buttons).
```

**Two aspects of encapsulation:**
1. **Bundling** — keeping related data and methods together in one class
2. **Hiding** — restricting direct access to internal data (data hiding)

---

## 2. Access Modifiers in Python

Python uses **naming conventions** (not strict keywords like Java/C++) to indicate access levels.

| Convention | Type | Symbol | Accessible from |
|---|---|---|---|
| `name` | Public | No prefix | Anywhere |
| `_name` | Protected | Single underscore | Class + subclasses (convention) |
| `__name` | Private | Double underscore | Class only (name mangled) |

---

## 3. Public Members

No underscore prefix. Accessible from anywhere — inside class, outside class, subclasses.

```python
class Student:
    def __init__(self, name, marks):
        self.name  = name    # public attribute
        self.marks = marks   # public attribute

    def display(self):       # public method
        print(f"{self.name}: {self.marks}")

s1 = Student("AJ", 85)

# Accessible from outside the class
print(s1.name)      # ✅ AJ
print(s1.marks)     # ✅ 85
s1.display()        # ✅ AJ: 85

# Can be modified directly
s1.marks = 100      # ✅ no restriction
print(s1.marks)     # 100
```

---

## 4. Protected Members — `_name`

Single underscore prefix. **Convention only** — Python doesn't enforce it. Signals "internal use — handle with care". Accessible by the class and its subclasses.

```python
class BankAccount:
    def __init__(self, owner, balance):
        self.owner    = owner       # public
        self._balance = balance     # protected

    def _calculate_interest(self):  # protected method
        return self._balance * 0.05

    def show(self):
        print(f"{self.owner}: ₹{self._balance}")

class SavingsAccount(BankAccount):
    def apply_interest(self):
        interest = self._calculate_interest()   # subclass accessing protected
        self._balance += interest
        print(f"Interest added. Balance: ₹{self._balance:.2f}")

acc = BankAccount("AJ", 10000)
print(acc._balance)   # ✅ Works — but signals "you shouldn't do this"
acc.show()

savings = SavingsAccount("Rahul", 20000)
savings.apply_interest()   # protected method used inside subclass
```

> **Key point:** Single underscore is a **gentleman's agreement** — Python won't stop you accessing it, but it communicates to other developers "this is internal". Respect it.

---

## 5. Private Members — `__name`

Double underscore prefix. Python applies **name mangling** — the attribute name is changed internally to `_ClassName__name`. This makes it very hard (not impossible) to access from outside.

```python
class BankAccount:
    def __init__(self, owner, balance, pin):
        self.owner    = owner        # public
        self._account = "ACC001"     # protected
        self.__balance = balance     # private
        self.__pin     = pin         # private

    def deposit(self, amount):
        if amount > 0:
            self.__balance += amount

    def withdraw(self, amount, pin):
        if pin != self.__pin:
            print("Wrong PIN!")
            return
        if amount > self.__balance:
            print("Insufficient balance")
            return
        self.__balance -= amount
        print(f"Withdrawn ₹{amount}. Balance: ₹{self.__balance}")

    def get_balance(self):           # controlled access to private data
        return self.__balance

acc = BankAccount("AJ", 10000, 1234)

print(acc.owner)         # ✅ AJ  — public
print(acc._account)      # ✅ ACC001  — protected (works but not ideal)

# print(acc.__balance)   # ❌ AttributeError: 'BankAccount' has no attribute '__balance'
# print(acc.__pin)       # ❌ AttributeError

# Correct way — use public methods
print(acc.get_balance())          # ✅ 10000
acc.withdraw(3000, 1234)          # ✅ Withdrawn ₹3000. Balance: ₹7000
acc.withdraw(3000, 9999)          # ✅ Wrong PIN!
```

---

## 6. Name Mangling — How Private Actually Works

Python doesn't truly make attributes private. It **renames** them to `_ClassName__attrname` internally.

```python
class Student:
    def __init__(self, name):
        self.__name = name   # stored as _Student__name

s1 = Student("AJ")

# print(s1.__name)              # ❌ AttributeError
print(s1._Student__name)        # ✅ AJ  — accessed via mangled name

# Check all attributes
print(s1.__dict__)
# Output: {'_Student__name': 'AJ'}
```

```python
# Name mangling prevents accidental override in subclasses
class Parent:
    def __init__(self):
        self.__value = 100   # stored as _Parent__value

class Child(Parent):
    def __init__(self):
        super().__init__()
        self.__value = 200   # stored as _Child__value — DIFFERENT from parent!

c = Child()
print(c.__dict__)
# {'_Parent__value': 100, '_Child__value': 200}
# Both exist independently — no collision!
```

> **Interview tip:** Name mangling is NOT the same as true private access. It is a mechanism to avoid name collisions in inheritance. The double underscore renames the attribute — it can still be accessed via the mangled name. Never use this in production code.

---

## 7. `@property` — Pythonic Encapsulation

`@property` lets you expose controlled access to private attributes with clean syntax — no `get_()` / `set_()` methods needed.

```python
class Employee:
    def __init__(self, name, salary):
        self.__name   = name
        self.__salary = salary

    @property
    def name(self):                     # getter
        return self.__name

    @name.setter
    def name(self, value):              # setter with validation
        if not isinstance(value, str) or len(value) == 0:
            raise ValueError("Name must be a non-empty string")
        self.__name = value

    @property
    def salary(self):
        return self.__salary

    @salary.setter
    def salary(self, value):
        if value < 0:
            raise ValueError("Salary cannot be negative")
        self.__salary = value

    @salary.deleter
    def salary(self):                   # deleter
        print("Salary data deleted")
        del self.__salary

    @property
    def annual_salary(self):            # computed — read-only property
        return self.__salary * 12

emp = Employee("AJ", 50000)

print(emp.name)             # Output: AJ         (calls getter)
print(emp.salary)           # Output: 50000       (calls getter)
print(emp.annual_salary)    # Output: 600000      (computed property)

emp.name   = "Gagan AJ"     # calls setter
emp.salary = 60000          # calls setter
print(emp.annual_salary)    # Output: 720000

emp.salary = -5000          # ❌ ValueError: Salary cannot be negative

del emp.salary              # Output: Salary data deleted (calls deleter)
```

---

## 8. `__slots__` — Restrict Attributes and Save Memory

By default, Python stores instance attributes in a `__dict__` for every object. For classes with many objects, this uses a lot of memory.

`__slots__` restricts which attributes an object can have and stores them more efficiently — no `__dict__` created.

```python
# Without __slots__ — uses __dict__ for every object
class StudentNormal:
    def __init__(self, name, marks):
        self.name  = name
        self.marks = marks

s1 = StudentNormal("AJ", 85)
s1.city = "Bengaluru"       # ✅ can add any attribute dynamically
print(s1.__dict__)           # {'name': 'AJ', 'marks': 85, 'city': 'Bengaluru'}


# With __slots__ — no __dict__, fixed attributes only
class StudentSlot:
    __slots__ = ["name", "marks"]   # only these attributes allowed

    def __init__(self, name, marks):
        self.name  = name
        self.marks = marks

s2 = StudentSlot("Rahul", 92)
print(s2.name)       # ✅ Rahul
print(s2.marks)      # ✅ 92

# s2.city = "Mumbai" # ❌ AttributeError: 'StudentSlot' has no attribute 'city'
# print(s2.__dict__) # ❌ AttributeError: no __dict__ with __slots__
```

**Memory comparison:**
```python
import sys

s1 = StudentNormal("AJ", 85)
s2 = StudentSlot("AJ", 85)

print(sys.getsizeof(s1))   # ~48 bytes + __dict__ overhead (~232 bytes total)
print(sys.getsizeof(s2))   # ~56 bytes — no __dict__ overhead
```

**When to use `__slots__`:**
- Creating millions of objects (data processing, simulations)
- Memory is constrained
- You know exactly which attributes the class needs

```python
# __slots__ with inheritance
class Animal:
    __slots__ = ["name", "sound"]

    def __init__(self, name, sound):
        self.name  = name
        self.sound = sound

class Dog(Animal):
    __slots__ = ["breed"]   # adds to parent's slots

    def __init__(self, name, breed):
        super().__init__(name, "Woof")
        self.breed = breed

d = Dog("Bruno", "Labrador")
print(d.name, d.sound, d.breed)   # Bruno Woof Labrador
```

---

## 9. Complete Encapsulation Example

A fully encapsulated `BankAccount` class combining everything:

```python
class BankAccount:
    __slots__ = ["_owner", "__balance", "__pin", "__transactions"]

    _bank_name = "Python Bank"   # class attribute — shared

    def __init__(self, owner, initial_balance, pin):
        self._owner         = owner
        self.__balance      = initial_balance
        self.__pin          = pin
        self.__transactions = []

    # --- Properties ---
    @property
    def owner(self):
        return self._owner

    @property
    def balance(self):
        return self.__balance

    @property
    def transaction_count(self):
        return len(self.__transactions)

    # --- Public methods ---
    def deposit(self, amount):
        if amount <= 0:
            raise ValueError("Deposit amount must be positive")
        self.__balance += amount
        self.__transactions.append(f"Deposit: +₹{amount}")
        print(f"Deposited ₹{amount}. Balance: ₹{self.__balance}")

    def withdraw(self, amount, pin):
        self.__verify_pin(pin)           # private method call
        if amount <= 0:
            raise ValueError("Withdrawal amount must be positive")
        if amount > self.__balance:
            raise ValueError("Insufficient balance")
        self.__balance -= amount
        self.__transactions.append(f"Withdrawal: -₹{amount}")
        print(f"Withdrawn ₹{amount}. Balance: ₹{self.__balance}")

    def get_statement(self):
        print(f"\n--- {self._bank_name} Statement for {self._owner} ---")
        for t in self.__transactions:
            print(f"  {t}")
        print(f"Current Balance: ₹{self.__balance}\n")

    # --- Private method ---
    def __verify_pin(self, pin):
        if pin != self.__pin:
            raise PermissionError("Invalid PIN")

    def __str__(self):
        return f"BankAccount({self._owner}, ₹{self.__balance})"


acc = BankAccount("AJ", 50000, 1234)
acc.deposit(10000)             # Deposited ₹10000. Balance: ₹60000
acc.withdraw(5000, 1234)       # Withdrawn ₹5000. Balance: ₹55000
acc.withdraw(1000, 9999)       # ❌ PermissionError: Invalid PIN
acc.get_statement()

print(acc.balance)             # ✅ 55000  — via property
print(acc.transaction_count)   # ✅ 2
# print(acc.__balance)         # ❌ AttributeError
```

---

## Quick Reference

```python
# ACCESS LEVELS
self.name    = value   # public   — accessible anywhere
self._name   = value   # protected — convention, accessible but "careful"
self.__name  = value   # private  — name mangled to _ClassName__name

# NAME MANGLING
# self.__attr  →  stored as  _ClassName__attr
# Access:  obj._ClassName__attr  (not recommended)

# PROPERTY
@property
def attr(self):
    return self.__attr               # getter — obj.attr

@attr.setter
def attr(self, val):
    self.__attr = val                # setter — obj.attr = val

@attr.deleter
def attr(self):
    del self.__attr                  # deleter — del obj.attr

# READ-ONLY property — only getter, no setter
@property
def computed(self):
    return self.__a + self.__b

# __slots__ — restrict and optimize
class MyClass:
    __slots__ = ["attr1", "attr2"]  # only these attributes allowed
    # no __dict__ created — faster, less memory
    # no dynamic attribute addition
```

---

## Interview Short Answers

**Q: What is encapsulation and why is it important?**
> Encapsulation is the OOP principle of bundling data and methods together inside a class and restricting direct access to internal data. It is important for two reasons: it protects data integrity by forcing access through validated methods — preventing invalid states like negative balances or empty names — and it hides implementation details so the internal workings can change without affecting code that uses the class.

**Q: What are the access modifiers in Python?**
> Python has three levels by convention. Public attributes have no prefix and are accessible from anywhere. Protected attributes have a single underscore prefix (`_name`) — Python doesn't enforce the restriction, but it signals to developers that the attribute is for internal use by the class and subclasses. Private attributes have a double underscore prefix (`__name`) — Python applies name mangling, renaming them to `_ClassName__name`, which prevents accidental access from outside.

**Q: What is name mangling in Python?**
> Name mangling is what Python does to attributes with a double underscore prefix. When you write `self.__balance` inside a class `BankAccount`, Python renames it internally to `self._BankAccount__balance`. This makes direct external access fail with an AttributeError. It also prevents name collisions in inheritance — a child class's `__value` and a parent's `__value` are stored separately. It is not true private access — the mangled name can still be used directly, but that is considered bad practice.

**Q: What is `@property` and what problem does it solve?**
> `@property` lets you expose a method as if it were an attribute. Without it, you need explicit getter and setter methods like `get_salary()` and `set_salary()`, which is verbose Java-style code. With `@property`, you can write `emp.salary` to call the getter and `emp.salary = 60000` to call the setter — clean attribute syntax with method-level control and validation. It also lets you add computed read-only properties like `annual_salary` without changing the public interface.

**Q: What is `__slots__` and when should you use it?**
> By default, Python stores instance attributes in a `__dict__` dictionary for each object, which uses memory and allows adding any attribute dynamically. `__slots__` replaces `__dict__` with a fixed set of attributes defined as a list — only those attributes can exist on the object. This reduces memory usage significantly when creating millions of objects, and prevents accidental dynamic attribute addition. Use it in data-heavy applications like simulations or large-scale data processing where memory matters.

**Q: What is the difference between protected and private attributes?**
> Both are conventions — Python does not enforce true access control at the language level. Protected (`_name`) uses a single underscore and signals "internal use" — it is accessible but developers should treat it as an implementation detail. Private (`__name`) uses double underscores and Python applies name mangling to make accidental access harder. Protected is used for attributes shared with subclasses. Private is for attributes strictly internal to one class. Neither is truly inaccessible — they are conventions that communicate intent.
