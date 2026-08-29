## **Python Basics - 1**

### **1. Variables in Python**
Variables in Python are used to store data values. They are created when you assign a value to them, and you don’t need to declare their type (Python is dynamically typed).

#### **Syntax for Variable Assignment:**
```python
x = 5  # Assigning an integer value to the variable x
y = "Hello"  # Assigning a string value to the variable y
```

#### **Variable Naming Rules:**
- Variable names can contain letters (a-z, A-Z), numbers (0-9), and underscores (_).
- Variable names must start with a letter or an underscore.
- Variable names are case-sensitive (`Name` and `name` are different).

#### **Example:**
```python
age = 25
name = "John"
is_student = True
```

### **2. Data Types in Python**
Python has various built-in data types. Some common ones are:
- **int**: For integers (e.g., 1, -3, 100)
- **float**: For floating-point numbers (e.g., 3.14, -0.001)
- **str**: For strings (e.g., "Hello", "Python")
- **bool**: For boolean values (True or False)

#### **Type Checking:**
You can use the `type()` function to check the type of a variable.
```python
x = 10
print(type(x))  # Output: <class 'int'>
```

### **3. Type Conversion**
Python allows you to convert between data types using functions like `int()`, `float()`, `str()`, etc.

#### **Example:**
```python
x = "10"  # x is a string
y = int(x)  # Convert string to integer
z = float(y)  # Convert integer to float
print(z)  # Output: 10.0
```

### **4. Arithmetic Operators**
Python supports basic arithmetic operations like addition, subtraction, multiplication, division, and more.

#### **Common Operators:**
- `+` (Addition)
- `-` (Subtraction)
- `*` (Multiplication)
- `/` (Division)
- `//` (Floor Division)
- `%` (Modulus)
- `**` (Exponentiation)

#### **Examples:**
```python
a = 10
b = 3
print(a + b)  # Output: 13(Addition)
print(a - b)  # Output: 7(Substraction)
print(a * b)  # Output: 30 (Multiplication)
print(a / b)  # Output: 3.3333...(True Division)
print(a // b)  # Output: 3 (Floor Division)
print(a % b)  # Output: 1 (Modulus)
print(a ** b)  # Output: 1000 (Exponentiation)
```
### **5. Assigning Values to Multiple Variables**
Python allows you to assign values to multiple variables in a single line.

#### **Example:**
```python
x, y, z = 10, 20, 30
print(x)  # Output: 10
print(y)  # Output: 20
print(z)  # Output: 30
```

You can also assign the same value to multiple variables in one line:
```python
x = y = z = 100
print(x, y, z)  # Output: 100 100 100
# simple assignment
a = 5

# chained assignment
b = c = 5

# multiple assignment
d,e = 1,2

# reassigning / swaping
g=a
```

### **6. Variable Reassignment**
You can change the value of a variable at any point in your program.

#### **Example:**
```python
x = 5
print(x)  # Output: 5
x = 10
print(x)  # Output: 10
```
----
----
# Python Variables and Object References

In Python, a variable is better understood as a **name that refers to an object** rather than a box that directly stores a value.

```text
Variable        Object

a ───────────→  10
```

Here:

- `a` → Variable / reference
- `10` → Object
- `10` is an `int` object

---

## 1. Assigning One Variable to Another

Consider:

```python
a = 10
b = a
```

Both `a` and `b` refer to the **same object**.

```text
        ┌───────┐
a ─────→│  10   │
        └───────┘
             ↑
b ───────────┘
```

We can check this using `is`:

```python
a = 10
b = a

print(a == b)   # True
print(a is b)   # True
```

- `==` → Checks whether the values are equal.
- `is` → Checks whether both variables refer to the same object.

---

## 2. Immutable Object

An **immutable object cannot be changed after it is created**.

Examples of immutable types include:

- `int`
- `float`
- `str`
- `tuple`

### Example with `int`

```python
a = 10
b = a
```

Initially:

```text
        ┌───────┐
a ─────→│  10   │
        └───────┘
             ↑
b ───────────┘
```

Now:

```python
b = 20
```

The `10` object is not changed.

Instead, `b` is reassigned to another object:

```text
        ┌───────┐
a ─────→│  10   │
        └───────┘

        ┌───────┐
b ─────→│  20   │
        └───────┘
```

Therefore:

```python
print(a)   # 10
print(b)   # 20
```

### Important

```python
b = 20
```

is **reassignment**, not modification of the integer `10`.

---

## 3. Mutable Object

A **mutable object can be changed after it is created**.

Examples include:

- `list`
- `set`
- `dict`

### Example with `list`

```python
a = [10, 20, 30]
b = a
```

Both variables refer to the same list:

```text
        ┌────────────────┐
a ─────→│ [10, 20, 30]   │
        └────────────────┘
             ↑
b ───────────┘
```

Now modify the list through `b`:

```python
b[0] = 100
```

The existing list is changed:

```text
        ┌─────────────────┐
a ─────→│ [100, 20, 30]   │
        └─────────────────┘
             ↑
b ───────────┘
```

Therefore:

```python
print(a)
print(b)
```

Output:

```text
[100, 20, 30]
[100, 20, 30]
```

Both variables see the change because they refer to the **same list object**.

---

## 4. Reassignment vs Modification

This distinction is very important.

### Reassignment

```python
a = [10, 20]
b = a

b = [30, 40]
```

Here, `b` is simply made to refer to a new list.

```text
a ─────→ [10, 20]

b ─────→ [30, 40]
```

The original list is not modified.

---

### Modification

```python
a = [10, 20]
b = a

b[0] = 100
```

Here, the existing list is modified.

```text
a ─────→ [100, 20]
             ↑
b ───────────┘
```

Both `a` and `b` see the modification.

---

## 5. `==` vs `is`

These operators have different purposes.

### `==` — Value Equality

```python
a = [10, 20]
b = [10, 20]

print(a == b)
```

Output:

```text
True
```

Why?

Because both lists contain the same values.

```text
a → [10, 20]
b → [10, 20]

Same contents → True
```

---

### `is` — Object Identity

```python
a = [10, 20]
b = [10, 20]

print(a is b)
```

Output:

```text
False
```

Why?

Because these are two separate list objects:

```text
        ┌────────────┐
a ─────→│ [10, 20]   │
        └────────────┘

        ┌────────────┐
b ─────→│ [10, 20]   │
        └────────────┘
```

They have the same contents, but they are **different objects**.

Therefore:

```python
a == b    # True
a is b    # False
```

---

## 6. Same Object vs Same Value

### Same object

```python
a = [10, 20]
b = a
```

```python
a == b    # True
a is b    # True
```

Both variables refer to the same object.

---

### Different objects with the same value

```python
a = [10, 20]
b = [10, 20]
```

```python
a == b    # True
a is b    # False
```

The values are equal, but the objects are different.

---

## 7. Mutable vs Immutable

| Type | Example | Mutable? |
|---|---|---|
| `int` | `10` | ❌ Immutable |
| `float` | `10.5` | ❌ Immutable |
| `str` | `"Python"` | ❌ Immutable |
| `tuple` | `(10, 20)` | ❌ Immutable |
| `list` | `[10, 20]` | ✅ Mutable |
| `set` | `{10, 20}` | ✅ Mutable |
| `dict` | `{"a": 10}` | ✅ Mutable |

---

## 8. The Main Mental Model

The most useful way to think about Python variables is:

```text
Variable → Reference → Object
```

For example:

```python
a = [10, 20, 30]
b = a
```

means:

```text
        ┌────────────────┐
a ─────→│ [10, 20, 30]   │
        └────────────────┘
             ↑
b ───────────┘
```

So:

> `b = a` means **"make `b` refer to the same object that `a` refers to."**

### Remember

- `==` → **Are the values equal?**
- `is` → **Are they the same object?**
- Mutable → **Object can be modified**
- Immutable → **Object cannot be modified**
- `b = a` → **Both refer to the same object**
- `b = new_value` → **Reassignment**
- `b[index] = new_value` → **Modification of a mutable object**
