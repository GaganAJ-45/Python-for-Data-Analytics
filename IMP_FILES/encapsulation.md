# Encapsulation in Python OOP

## 1. What Is Encapsulation?

**Encapsulation is one of the four fundamental principles of Object-Oriented Programming (OOP).**

The four principles are:

1. Encapsulation
2. Abstraction
3. Inheritance
4. Polymorphism

Encapsulation means **combining data (attributes) and the methods that operate on that data inside a single class, while controlling how the data is accessed and modified.**

For example, consider a bank account.

A bank account contains:

* Account holder's name
* Account number
* Account balance

The account balance should not be modified carelessly. A bank should be able to control how the balance is accessed and updated.

Python allows us to implement this idea using classes, naming conventions, name mangling, and methods such as getters and setters.

---

## 2. Example: Bank Class

Consider the following Python program:

```python
class Bank:
    def __init__(self, owner, account, balance):
        self.owner = owner
        self._account = account
        self.__balance = balance

    def get_balance(self):
        return self.__balance

    def set__balance(self, balance):
        self.__balance = balance


al = Bank("hmz", 321, 565656)

print(al.owner)
print(al._account)
print(al.get_balance())

print("after")

al.set__balance(50000)

print(al.get_balance())
```

### Output

```text
hmz
321
565656
after
50000
```

Let's understand how encapsulation works in this example.

---

## 3. Understanding the Constructor (`__init__`)

```python
def __init__(self, owner, account, balance):
    self.owner = owner
    self._account = account
    self.__balance = balance
```

The `__init__()` method initializes the attributes of the object when it is created.

When we execute:

```python
al = Bank("hmz", 321, 565656)
```

Python initializes the object with these values:

| Attribute   | Value    | Access convention        |
| ----------- | -------- | ------------------------ |
| `owner`     | `"hmz"`  | Public                   |
| `_account`  | `321`    | Protected by convention  |
| `__balance` | `565656` | Private by name mangling |

The three attributes demonstrate different naming conventions in Python.

---

## 4. Types of Attributes in Python

### 4.1 Public Attributes

A public attribute can be accessed directly from outside the class.

In our example:

```python
self.owner = owner
```

We can access it using:

```python
print(al.owner)
```

Output:

```text
hmz
```

We can also modify it directly:

```python
al.owner = "raj"

print(al.owner)
```

Output:

```text
raj
```

**Key point:** Public attributes do not restrict direct access or modification.

### 4.2 Protected Attributes

A single leading underscore indicates that an attribute is intended for internal use.

In our example:

```python
self._account = account
```

We can still access it directly:

```python
print(al._account)
```

Output:

```text
321
```

We can even modify it:

```python
al._account = 999

print(al._account)
```

Output:

```text
999
```

Python does not enforce protected access for attributes with a single leading underscore.

The underscore is a convention that communicates:

> This attribute is intended for internal use. Access it directly only when you understand the implications.

**Key point:** A single underscore indicates intended internal use, not enforced access restriction.

### 4.3 Private Attributes

A double leading underscore triggers a Python feature called **name mangling**.

In our example:

```python
self.__balance = balance
```

Now try:

```python
print(al.__balance)
```

Python raises an error similar to:

```text
AttributeError: 'Bank' object has no attribute '__balance'
```

Why?

Python internally changes the attribute name from:

```python
__balance
```

to:

```python
_Bank__balance
```

Therefore, this statement works:

```python
print(al._Bank__balance)
```

Output:

```text
565656
```

However, accessing a private attribute this way is generally discouraged.

**Key point:** Double underscores help prevent accidental access and naming conflicts. They do not provide absolute privacy or security.

---

## 5. What Are Getters and Setters?

Getters and setters are methods used to read and modify an attribute through the class.

They are useful when we want to control access to an object's internal data.

### 5.1 Getter Method

Our example contains:

```python
def get_balance(self):
    return self.__balance
```

A getter retrieves the current balance.

We call it using:

```python
print(al.get_balance())
```

Output:

```text
565656
```

The getter can access `self.__balance` because it is defined inside the `Bank` class.

The getter provides a controlled way to retrieve the balance without accessing the attribute directly.

### 5.2 Setter Method

Our example contains:

```python
def set__balance(self, balance):
    self.__balance = balance
```

A setter modifies the balance.

We call it using:

```python
al.set__balance(50000)
```

The method assigns the new value to the private attribute.

Now:

```python
print(al.get_balance())
```

Output:

```text
50000
```

The balance changes from `565656` to `50000`.

Notice that the original method is named `set__balance()` with two underscores between `set` and `balance`. It works, but `set_balance()` is a more conventional name.

### Why Use a Setter?

Consider this statement:

```python
al.set__balance(-5000)
```

Your original setter accepts the negative balance because it does not perform validation.

This demonstrates an important point:

**Using a setter does not automatically make an attribute safe. The setter must enforce the rules you need.**

We can improve it:

```python
def set_balance(self, balance):
    if balance >= 0:
        self.__balance = balance
    else:
        print("Balance cannot be negative")
```

Now, the setter rejects negative balances.

For example:

```python
al.set_balance(50000)
print(al.get_balance())

al.set_balance(-5000)
print(al.get_balance())
```

Output:

```text
50000
Balance cannot be negative
50000
```

The second update does not change the balance.

---

## 6. How Encapsulation Works Step by Step

Let's examine the execution of the original program.

### Step 1: Create the Object

```python
al = Bank("hmz", 321, 565656)
```

The `Bank` constructor initializes the object's attributes.

The object contains:

```text
owner      = "hmz"
_account   = 321
__balance  = 565656
```

Internally, the private attribute is stored under the name `_Bank__balance`.

### Step 2: Access the Public Attribute

```python
print(al.owner)
```

Output:

```text
hmz
```

The attribute can be accessed directly.

### Step 3: Access the Protected-by-Convention Attribute

```python
print(al._account)
```

Output:

```text
321
```

Python permits direct access because the single underscore does not enforce access restrictions.

### Step 4: Read the Private Attribute Through a Getter

```python
print(al.get_balance())
```

Output:

```text
565656
```

The getter retrieves the balance from inside the class.

### Step 5: Update the Balance Through a Setter

```python
al.set__balance(50000)
```

The setter assigns the new balance.

The internal value changes from:

```text
565656
```

to:

```text
50000
```

### Step 6: Read the Updated Balance

```python
print(al.get_balance())
```

Output:

```text
50000
```

The getter returns the updated value.

---

## 7. What Happens If We Modify `__balance` Directly?

Consider:

```python
al = Bank("hmz", 321, 565656)

al.__balance = 20000

print(al.get_balance())
```

Output:

```text
565656
```

Why does it still return `565656`?

Because:

```python
al.__balance = 20000
```

creates a separate attribute named `__balance` on the instance. Outside the class, Python does not automatically interpret that assignment as a modification of `_Bank__balance`.

The actual balance remains stored in:

```python
al._Bank__balance
```

Therefore, the getter continues to return `565656`.

This example demonstrates how name mangling helps prevent accidental modification of the original private attribute.

However, name mangling is not a security mechanism. Python still allows direct access to `_Bank__balance`.

---

## 8. Why Is Encapsulation Important?

Encapsulation offers several benefits.

### 8.1 Data Protection Against Accidental Modification

Using a double-underscore attribute helps prevent accidental direct access.

```python
self.__balance = balance
```

This is useful when a class maintains internal state that should not be modified casually.

### 8.2 Controlled Modification

A setter allows us to apply rules before changing a value.

For example:

```python
def set_balance(self, balance):
    if balance >= 0:
        self.__balance = balance
    else:
        print("Invalid balance")
```

This allows the class to reject invalid values.

### 8.3 Maintainability

Suppose the bank introduces a rule that the balance cannot be negative.

If all balance updates go through a validated setter, we can implement the rule in one place rather than repeating it throughout the application.

### 8.4 Better Control Over Object State

A class can decide which operations are permitted.

For example, instead of allowing arbitrary balance changes, a more realistic banking class could provide methods such as:

```python
deposit(amount)
withdraw(amount)
get_balance()
```

Each method could enforce the appropriate business rules.

This is more meaningful than exposing a setter that allows any non-negative balance to be assigned.

---

## 9. Improved Bank Class

The original example demonstrates encapsulation, but its setter can accept invalid values, and its name is unconventional.

Here is an improved version:

```python
class Bank:
    def __init__(self, owner, account, balance):
        if balance < 0:
            raise ValueError("Initial balance cannot be negative")

        self.owner = owner
        self._account = account
        self.__balance = balance

    def get_balance(self):
        return self.__balance

    def set_balance(self, balance):
        if balance < 0:
            print("Balance cannot be negative")
            return

        self.__balance = balance


al = Bank("hmz", 321, 565656)

print(al.owner)
print(al._account)
print(al.get_balance())

print("After updating balance:")

al.set_balance(50000)
print(al.get_balance())

print("Attempting an invalid update:")

al.set_balance(-5000)
print(al.get_balance())
```

### Output

```text
hmz
321
565656
After updating balance:
50000
Attempting an invalid update:
Balance cannot be negative
50000
```

This version:

* Rejects a negative initial balance.
* Uses a private attribute for the balance.
* Provides a getter to read the balance.
* Provides a setter that validates the new value.
* Preserves the existing balance when an invalid update is attempted.

**Important:** This is still a simplified example. Real banking systems require additional controls, such as transaction validation, concurrency handling, authorization, and reliable transaction records.

---

## 10. Encapsulation vs. Data Hiding

These terms are related but not identical.

| Encapsulation                                                         | Data Hiding                                                 |
| --------------------------------------------------------------------- | ----------------------------------------------------------- |
| Combines data and related methods within a class.                     | Restricts or discourages direct access to internal details. |
| Focuses on organizing and controlling an object's state and behavior. | Focuses on limiting access to implementation details.       |
| Can be implemented using classes and methods.                         | In Python, conventions and name mangling help support it.   |

Encapsulation can involve data hiding, but encapsulation is broader than simply making an attribute private.

---

## 11. Important Interview Questions

### Q1. What is encapsulation in Python?

Encapsulation is an OOP principle that combines data and the methods operating on that data within a class and allows controlled access to the object's internal state.

### Q2. Why do we use `__balance` instead of `balance`?

The double leading underscore triggers name mangling. This helps prevent accidental access and naming conflicts.

### Q3. Does Python support private variables?

Python does not enforce strict private access in the same way as some other languages. Double-underscore attributes undergo name mangling, but they can still be accessed through their mangled names.

### Q4. What is the difference between `_account` and `__balance`?

`_account` uses a single leading underscore, which conventionally indicates internal use.

`__balance` uses a double leading underscore, which triggers name mangling.

Neither naming style provides absolute security.

### Q5. What is a getter?

A getter is a method that retrieves an attribute's value.

Example:

```python
def get_balance(self):
    return self.__balance
```

### Q6. What is a setter?

A setter is a method that modifies an attribute's value, potentially after validation.

Example:

```python
def set_balance(self, balance):
    if balance >= 0:
        self.__balance = balance
```

### Q7. Does encapsulation require getters and setters?

No. Getters and setters are one approach to controlling access, but they are not mandatory. Python also supports properties, which can provide controlled attribute access.

### Q8. Can we access `__balance` outside the class?

Not directly through `al.__balance` when the attribute was defined as `self.__balance` inside `Bank`.

However, name mangling changes the internal name to `_Bank__balance`, which can still be accessed.

### Q9. What is the main advantage of encapsulation?

It helps manage an object's internal state, centralize validation, reduce accidental modification, and make code easier to maintain.

---

## 12. Key Takeaways

* Encapsulation is one of the four fundamental OOP principles.
* It combines data and related methods within a class.
* Public attributes can be accessed directly.
* A single leading underscore indicates intended internal use by convention.
* A double leading underscore triggers name mangling.
* Getters retrieve values.
* Setters modify values and can validate input.
* Getters and setters do not automatically guarantee data safety.
* Name mangling is not a security mechanism.
* Encapsulation is about controlling and managing an object's state, not merely hiding variables.

**Final concept:**

In the `Bank` class, `__balance` represents the internal state, `get_balance()` provides a way to read it, and `set__balance()` provides a way to modify it.

That is the central idea behind encapsulation in this example.
