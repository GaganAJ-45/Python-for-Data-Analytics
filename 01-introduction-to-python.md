# Introduction to Python Programming
> Foundation Notes — Interview Ready

---

## 1. What is Python?

Python is a **high-level, interpreted, dynamically typed, and object-oriented** programming language known for its simplicity and readability. It allows developers to write clear programs for both small and large-scale projects.

```python
print("Hello, World!")  # Your first Python program
```

---

## 2. Where is Python Used?

| Domain | Examples |
|---|---|
| Web Development | Django, Flask |
| Data Science & Analytics | Pandas, NumPy |
| Machine Learning & AI | TensorFlow, PyTorch, Scikit-learn |
| Automation & Scripting | File handling, web scraping |
| Software Development | General-purpose applications |
| Trading & Finance | Algorithmic trading, financial modeling |

---

## 3. Why is Python Popular?

- **Easy to learn** — Syntax is simple and close to natural English
- **Large community** — Tons of tutorials, libraries, and support
- **Cross-platform** — Runs on Windows, macOS, and Linux
- **Versatile** — Whether it's web development, data analysis, or automation, Python has libraries for almost everything
- **Rich Standard Library** — Comes with hundreds of built-in modules

---

## 4. Advantages and Disadvantages

### Advantages
- Simple, readable syntax — fast to write and understand
- Huge ecosystem of libraries
- Great for rapid prototyping
- Strong community support
- Free and open source

### Disadvantages
- **Slow execution speed** — interpreted line by line, much slower than C or Java
- **High memory usage** — not ideal for memory-intensive tasks
- **GIL (Global Interpreter Lock)** — limits true multi-threading in CPython
- **Weak in mobile development** — not a primary language for mobile apps
- **Runtime errors** — dynamic typing means type errors only show up at runtime, not before running

---

## 5. Key Features of Python

### 5.1 High-Level Language
Python hides low-level hardware details. You don't manage CPU registers or memory addresses directly — Python handles that for you.

```python
age = 22
print(age)
# No need to manage memory, pointers, or data types explicitly
```

> **High-Level = Human-readable syntax + abstraction from hardware**

---

### 5.2 Interpreted Language (Compiled + Interpreted)

This is a **very common interview question.**

> *"Is Python compiled or interpreted?"*

**Answer:** Python is **both** — it goes through two stages:

```
Source Code (.py)
       ↓
  Python Compiler
       ↓
  Bytecode (.pyc)         ← stored in __pycache__ folder
       ↓
Python Virtual Machine (PVM)
       ↓
   Output
```

1. Your `.py` file is first **compiled** into **bytecode** (`.pyc` files)
2. That bytecode is then **interpreted** line by line by the **Python Virtual Machine (PVM)**

So Python is not purely interpreted — it compiles to bytecode first, then interprets it.

**Benefits of this approach:**
- Easier debugging — errors reported line by line
- Faster development — no manual compile step needed
- Bytecode is reused on subsequent runs (faster startup)

---

### 5.3 Dynamically Typed

In Python, you **don't need to declare the type** of a variable. The type is decided at **runtime** based on the value assigned.

```python
# Python — dynamically typed
x = 10        # x is int
x = "hello"   # now x is str — Python allows this
x = [1, 2, 3] # now x is list — still fine

print(type(x))  # Output: <class 'list'>
```

Compare with a **statically typed** language like Java:
```java
// Java — statically typed
int x = 10;      // type is fixed at declaration
x = "hello";     // ERROR — cannot change type
```

> **Interview answer:** *"Python is dynamically typed, meaning variable types are determined at runtime, not at compile time. You don't need to declare types explicitly, but this also means type errors only appear when the code actually runs."*

---

### 5.4 Object-Oriented Language

Python supports **Object-Oriented Programming (OOP)** — organizing code around objects and classes.

```python
class Student:
    def __init__(self, name):
        self.name = name

    def study(self):
        print(self.name, "is studying")

student1 = Student("AJ")
student1.study()   # Output: AJ is studying
```

| Term | Meaning |
|---|---|
| **Class** | Blueprint for creating objects |
| **Object** | Instance of a class |
| **Attribute** | Data/property of an object |
| **Method** | Function defined inside a class |

**4 main OOP concepts:**
- **Encapsulation** → Bundling data and methods together
- **Inheritance** → One class reusing properties of another
- **Polymorphism** → Same interface, different behavior
- **Abstraction** → Hiding internal implementation details

> Python is **multi-paradigm** — it also supports procedural and functional programming styles.

---

### 5.5 Platform Independent

The same Python source code runs on different operating systems as long as a Python interpreter is installed.

```
   Python Code (.py)
          ↓
   Python Interpreter
          ↓
  ┌───────┼───────┐
  ↓       ↓       ↓
Windows  Linux  macOS
```

```python
print("Hello World")
# This exact code runs identically on Windows, Linux, and macOS
```

> **Note:** OS-specific code, file paths, or certain libraries may still need adjustment across platforms.

---

### 5.6 Multi-Paradigm

Python supports multiple programming styles:

| Style | Meaning | Example |
|---|---|---|
| **Procedural** | Step-by-step instructions | Functions, loops |
| **Object-Oriented** | Code organized around objects | Classes, inheritance |
| **Functional** | Functions as first-class citizens | `map()`, `filter()`, `lambda` |

---

## 6. Compiled vs Interpreted — Full Comparison

| Feature | Compiled (C, Java) | Interpreted (Python) |
|---|---|---|
| Translation | Entire code at once | Line by line |
| Speed | Faster execution | Slower execution |
| Error detection | Before running | During running |
| Output | Machine code / bytecode | Direct output |
| Example | GCC for C | CPython for Python |

> Python sits in the middle — compiles to bytecode, then interprets it.

---

## 7. PEP 8 — Python Style Guide

**PEP** stands for **Python Enhancement Proposal**. **PEP 8** is the official **style guide** for writing clean, readable Python code.

> *"What is PEP 8?"* — this comes up in interviews to check if you write professional code.

### Key PEP 8 Rules:

```python
# 1. Use snake_case for variable and function names
student_name = "AJ"        # ✅ correct
studentName = "AJ"         # ❌ avoid (camelCase is for Java)

# 2. Use PascalCase for class names
class StudentProfile:      # ✅ correct
    pass

# 3. Use UPPER_CASE for constants
MAX_SIZE = 100             # ✅ correct

# 4. Use 4 spaces for indentation (not tabs)
def greet():
    print("Hello")         # ✅ 4 spaces

# 5. Maximum 79 characters per line
# 6. Two blank lines between top-level functions/classes
# 7. One blank line between methods inside a class
# 8. Imports go at the top of the file
import os
import sys
```

> **Why it matters:** PEP 8 makes your code consistent and readable for teams. Most companies expect you to follow it.

---

## 8. Python Versions

| Version | Status |
|---|---|
| Python 2.x | ❌ End of life (Jan 2020) — do not use |
| Python 3.x | ✅ Current — always use this |

> Always use **Python 3**. Python 2 is dead. The key difference: `print` is a function in Python 3 (`print()`), a statement in Python 2 (`print`).

---

## Quick Summary Table

| Feature | What it means |
|---|---|
| High-Level | Human-readable, hides hardware details |
| Interpreted | Compiled to bytecode → executed by PVM |
| Dynamically Typed | Types decided at runtime, no declarations needed |
| Object-Oriented | Supports classes, objects, OOP principles |
| Platform Independent | Same code runs on Windows, Linux, macOS |
| Multi-Paradigm | Supports procedural, OOP, and functional styles |

---

## Interview Short Answers

**Q: What is Python?**
> Python is a high-level, interpreted, dynamically typed, and object-oriented programming language. It is known for its simple syntax, large standard library, and versatility across web development, data science, automation, and more.

**Q: Is Python compiled or interpreted?**
> Python is both. Source code is first compiled into bytecode by the Python compiler, then that bytecode is executed line by line by the Python Virtual Machine (PVM). The bytecode is stored in `.pyc` files inside the `__pycache__` folder.

**Q: What does dynamically typed mean?**
> It means variable types are determined at runtime based on the value assigned. You don't need to declare types explicitly. The same variable can hold different types at different points in the program.

**Q: What is PEP 8?**
> PEP 8 is Python's official style guide. It defines rules for writing clean, consistent, and readable Python code — such as using snake_case for variables, PascalCase for classes, 4 spaces for indentation, and keeping lines under 79 characters.

**Q: What are the disadvantages of Python?**
> Python is slower than compiled languages like C or Java due to its interpreted nature. It also has high memory usage, a GIL that limits true multi-threading, and is not well-suited for mobile development.
