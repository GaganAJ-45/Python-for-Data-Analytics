# Python Practice: Data Types, Type Conversion & Strings

Daily practice problems on Python's built-in data types, type conversion, and string handling.

Click a question to jump straight to its solution and sample output. Try solving it yourself first! If you spot a bug, have a better approach, or have a doubt about any solution — open an issue or drop a comment.

## Questions

1. [Create a complex number and print its real and imaginary parts, and its type.](#1-complex-numbers)
2. [Convert values between `int`, `str`, `float`, and `complex` and check their types.](#2-type-conversion)
3. [Take a name, USN, and salary as input with appropriate types.](#3-typed-user-input)
4. [Convert numbers between binary, octal, hexadecimal, and decimal.](#4-number-base-conversion)
5. [Combine variables into a sentence using both string concatenation and f-strings.](#5-string-concatenation-vs-f-strings)
6. [Demonstrate the difference between mutable (list) and immutable (int) objects with `+=`.](#6-mutable-vs-immutable-behavior)
7. [Print all Python keywords and count how many there are.](#7-python-keywords)
8. [Demonstrate simple, chained, and multiple assignment.](#8-assignment-styles)
9. [Join a list of characters into a single string.](#9-join-characters-into-a-string)
10. [Count the number of vowels in a string.](#10-count-vowels-in-a-string)
11. [Check whether a string is a palindrome.](#11-palindrome-check)
12. [Reverse each word in a sentence (keep word order, reverse the letters in each word).](#12-reverse-each-word-in-a-sentence)

---

## Solutions

### 1. Complex Numbers
```python
num1 = 2 + 3j
print(num1)
print(type(num1))
print(num1.real)
print(num1.imag)
```
**Output:**
```
(2+3j)
<class 'complex'>
2.0
3.0
```

### 2. Type Conversion
```python
a = 5
b = 'Gagan A J'
c = 3.14
d = '123456'
e = '2+3j'

f = int(d)
print(f)
print(type(f))

g = str(a)
print(type(g))

f = float(f)
print(f)
print(type(f))

h = 12345
i = complex(h)
print(i)

j = 32.232
k = str(j)
print(k)
print(type(k))
```
**Output:**
```
123456
<class 'int'>
<class 'str'>
123456.0
<class 'float'>
(12345+0j)
32.232
<class 'str'>
```

### 3. Typed User Input
```python
name = input("Enter your name: ")
print(name)
print(type(name))

USN = int(input("Enter your USN: "))
print(USN)
print(type(USN))

salary = float(input("Enter your salary: "))
print(salary)
print(type(salary))
```
**Sample input:** `Gagan`, `123`, `50000.5`
**Output:**
```
Gagan
<class 'str'>
123
<class 'int'>
50000.5
<class 'float'>
```

### 4. Number Base Conversion
```python
a = int(0b1011010)      # binary literal -> decimal
b = int(0o132)           # octal literal -> decimal
c = int(0x5a)             # hex literal -> decimal
d = int("10110", 2)      # binary string -> decimal
e = int("132", 8)        # octal string -> decimal
f = int("21a", 16)       # hex string -> decimal

print(a)
print(b)
print(c)
print(d)
print(e)
print(f)
```
**Output:**
```
90
90
90
22
90
538
```

### 5. String Concatenation vs f-strings
```python
name = "gagan"
init = "python"
age = "16"

print("i am a " + init + " developer and my name is " + name)
print(f"i am a {init} developer and my name is {name} and i am {age} years old")
```
**Output:**
```
i am a python developer and my name is gagan
i am a python developer and my name is gagan and i am 16 years old
```

### 6. Mutable vs Immutable Behavior
```python
# With a list (mutable) - += modifies the SAME object in place
a = [1, 2, 3]
b = a
a += [4]
print(a, b)  # b changes too, since a and b point to the same list

# With an int (immutable) - += creates a NEW object
x = 5
y = x
x += 1
print(x, y)  # y is unaffected, since x now points to a new int
```
**Output:**
```
[1, 2, 3, 4] [1, 2, 3, 4]
6 5
```

### 7. Python Keywords
```python
import keyword
kw = keyword.kwlist
print(kw)
print(len(kw))
```
**Output:**
```
['False', 'None', 'True', 'and', 'as', 'assert', 'async', 'await', 'break', 'class', 'continue', 'def', 'del', 'elif', 'else', 'except', 'finally', 'for', 'from', 'global', 'if', 'import', 'in', 'is', 'lambda', 'nonlocal', 'not', 'or', 'pass', 'raise', 'return', 'try', 'while', 'with', 'yield']
35
```
> Note: the exact count can vary slightly by Python version (soft keywords like `match`/`case`/`_` are listed separately via `keyword.softkwlist`). This output is from Python 3.12.

### 8. Assignment Styles
```python
# simple assignment
a = 5

# chained assignment
b = c = 5

# multiple assignment
d, e = 1, 2

print(a)
print(b, c)
print(d, e)
```
> Note: added `print()` calls — the original only assigned the variables with no output to show.

**Output:**
```
5
5 5
1 2
```

### 9. Join Characters into a String
```python
l = ["P", "Y", "T", "H", "O", "N"]
print("".join(l))
```
**Output:**
```
PYTHON
```

### 10. Count Vowels in a String
```python
t = "welcome to python"
x = t.lower()
a = x.count("a")
b = x.count("e")
c = x.count("i")
d = x.count("o")
e = x.count("u")

total = a + b + c + d + e
print(total)
```
**Output:**
```
5
```

### 11. Palindrome Check
```python
a = "madam"
b = a[::-1]
print(a == b)   # True if palindrome, False otherwise
```
> Note: added the actual comparison — the original only reversed the string and printed it, without checking whether it matches the original.

**Output:**
```
True
```

### 12. Reverse Each Word in a Sentence
```python
text = "I love Python"
words = text.split()
reversed_words = [word[::-1] for word in words]
result = " ".join(reversed_words)
print(result)
```
> ⚠️ This one was incomplete in your code (only the `text` variable was set, no logic yet) — I've added a solution using `split()`, a reversed slice per word, and `join()`. Let me know if you were going for a different approach (e.g. a loop instead of a list comprehension) and I'll adjust it.

**Output:**
```
I evol nohtyP
```
