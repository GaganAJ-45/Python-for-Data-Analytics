## **Input/Output, String Manipulation, and Comments**

### **1. Input and Output in Python**

#### **1.1 Input from the User:**
In Python, we use the `input()` function to take input from the user. The data entered by the user is always received as a string, so if you want to use it as a different data type (e.g., integer or float), you'll need to convert it using type conversion functions like `int()` or `float()`.

```python
name1 = input("Enter your name: ")
age = int(input("Enter your age: "))  # Convert input to integer

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

#### **1.2 Output to the Console:**
The `print()` function is used to display output to the console. You can use it to display text, variables, or results of expressions.

```python
print("Hello, " + name + "! You are " + str(age) + " years old.")
```

You can also use **f-strings** (formatted string literals) for more readable code:
```python
print(f"Hello, {name}! You are {age} years old.")
```
---
# String Manipulation in Python

## What is a String?

A string is a **sequence of characters** enclosed in:
- Single quotes `' '`
- Double quotes `" "`
- Triple quotes `''' '''` or `""" """` (used for multi-line strings)

```python
name = 'Aj'
city = "Bengaluru"
bio = """I am a Python developer
from Bengaluru."""
```

**String manipulation** means performing operations on strings such as:
- Reading characters
- Extracting parts
- Searching
- Replacing
- Joining / Splitting
- Changing case
- Removing spaces

---

## 2.1 Common String Operations

### Concatenation (`+`)
Joining two or more strings together.

**Where to use:** Building full names, sentences, file paths, messages.

```python
first_name = "John"
last_name = "Doe"
full_name = first_name + " " + last_name
print(full_name)  # Output: John Doe
```

---

### Repetition (`*`)
Repeating a string multiple times.

**Where to use:** Creating separators, patterns, repeated messages.

```python
greeting = "Hello! " * 3
print(greeting)  # Output: Hello! Hello! Hello!

print("-" * 30)  # Output: ------------------------------ (divider line)
```

---

## 2.2 String Methods

---

### `len()`
Returns the **total number of characters** in a string, including spaces and symbols.

**Where to use:** Validating input length (e.g., password must be 8+ characters), counting characters.

```python
message = "  Hello, World!  "
print(len(message))  # Output: 18

# Why 18? Count every character including the 2 spaces on each side:
# _ _ H e l l o ,   W o r l d ! _ _  = 18 characters
```

---

### `upper()`
Converts **all characters** in the string to uppercase.

**Where to use:** Standardizing user input, displaying headings, comparing strings case-insensitively.

```python
name = "aj kumar"
print(name.upper())  # Output: AJ KUMAR

# Real use: case-insensitive comparison
user_input = "yes"
if user_input.upper() == "YES":
    print("Confirmed!")  # Output: Confirmed!
```

---

### `lower()`
Converts **all characters** in the string to lowercase.

**Where to use:** Normalizing emails, usernames, search queries.

```python
email = "AJ.KUMAR@GMAIL.COM"
print(email.lower())  # Output: aj.kumar@gmail.com

# Real use: storing emails in a consistent format
```

---

### `swapcase()`
**Swaps** every uppercase letter to lowercase and every lowercase letter to uppercase.

**Where to use:** Text formatting effects, toggling case for stylistic output.

```python
text = "Hello World"
print(text.swapcase())  # Output: hELLO wORLD

text2 = "aJ kUmAr"
print(text2.swapcase())  # Output: Aj KuMaR
```

---

### `capitalize()`
Converts the **first character** of the string to uppercase and the **rest to lowercase**.

**Where to use:** Formatting names or sentences where only the first letter should be capitalized.

```python
name = "aj kumar"
print(name.capitalize())  # Output: Aj kumar
#                                         ^ rest stays lowercase

sentence = "pYTHON IS FUN"
print(sentence.capitalize())  # Output: Python is fun
```

---

### `title()`
Converts the **first character of every word** to uppercase.

**Where to use:** Formatting full names, book titles, headings.

```python
name = "aj kumar"
print(name.title())  # Output: Aj Kumar

title = "introduction to python programming"
print(title.title())  # Output: Introduction To Python Programming
```

---

### `strip()`
Removes **leading and trailing spaces** (both sides) from a string.

**Where to use:** Cleaning user input from forms, reading data from files where extra spaces creep in.

```python
message = "  Hello, World!  "
print(message.strip())   # Output: Hello, World!
#            ^ spaces removed from both left and right sides
```

---

### `lstrip()`
Removes spaces only from the **left side** (leading spaces).

**Where to use:** When you want to clean only the beginning of a string.

```python
message = "  Hello, World!  "
print(message.lstrip())  # Output: Hello, World!  
#                                               ^^ trailing spaces still present
```

---

### `rstrip()`
Removes spaces only from the **right side** (trailing spaces).

**Where to use:** Cleaning line endings when reading text files.

```python
message = "  Hello, World!  "
print(message.rstrip())  # Output:   Hello, World!
#                                    ^^ leading spaces still present
```

---

### `replace(old, new)`
Replaces **all occurrences** of a substring with another string.

**Where to use:** Censoring words, fixing typos in bulk, formatting text.

```python
message = "  Hello, World!  "
print(message.replace("World", "Python"))
# Output:   Hello, Python!  
# Note: the leading/trailing spaces are still there since we only replaced "World"

sentence = "I love Java. Java is great."
print(sentence.replace("Java", "Python"))
# Output: I love Python. Python is great.

# Replace all spaces with underscores (useful for filenames)
filename = "my project file"
print(filename.replace(" ", "_"))  # Output: my_project_file
```

---

### `split(sep)`
Splits a string into a **list of substrings** using a separator. Default separator is whitespace.

**Where to use:** Parsing CSV data, breaking a sentence into words, splitting a path by `/`.

```python
sentence = "python is fun and python is powerful"

print(sentence.split())           # Output: ['python', 'is', 'fun', 'and', 'python', 'is', 'powerful']
# Default: splits on every space

print(sentence.split("and"))      # Output: ['python is fun ', ' python is powerful']
# Splits wherever "and" appears

csv_data = "Aj,Kumar,Bengaluru,Python"
print(csv_data.split(","))        # Output: ['Aj', 'Kumar', 'Bengaluru', 'Python']
```

---

### `join(iterable)`
**Opposite of split.** Joins elements of a list into a single string, using the string as a separator.

**Where to use:** Building sentences from word lists, creating CSV rows, constructing file paths.

```python
words = ["Learn", "Python", "Fast"]
print(" ".join(words))    # Output: Learn Python Fast
#      ^ space is the separator

print("-".join(words))    # Output: Learn-Python-Fast

# Joining a list back after split
parts = ["Aj", "Kumar", "Bengaluru"]
print(", ".join(parts))   # Output: Aj, Kumar, Bengaluru
```

---

### `count(sub)`
Returns the **number of times** a substring appears in the string.

**Where to use:** Counting word frequency, finding repeated patterns.

```python
sentence = "python is fun and python is powerful"
print(sentence.count("python"))   # Output: 2
print(sentence.count("is"))       # Output: 2

text = "banana"
print(text.count("a"))            # Output: 3
```

---

### `find(sub)`
Returns the **index of the first occurrence** of a substring.
Returns `-1` if the substring is **not found** (does NOT raise an error).

**Where to use:** Checking if a word exists in text, finding position before slicing.

```python
text = "Programming"
print(text.find("g"))    # Output: 3   (first 'g' is at index 3)
print(text.find("z"))    # Output: -1  (not found, returns -1 safely)

sentence = "I love Python"
print(sentence.find("Python"))   # Output: 7
print(sentence.find("Java"))     # Output: -1
```

---

### `rfind(sub)`
Same as `find()` but searches from the **right side** (finds the **last occurrence**).

**Where to use:** Finding the last occurrence of a character, like the last `/` in a file path.

```python
text = "Programming"
print(text.rfind("g"))    # Output: 10  (last 'g' is at index 10)

path = "/home/aj/projects/app.py"
print(path.rfind("/"))    # Output: 16  (last slash, before filename)
```

> ⚠️ Note: `lfind()` does **not exist** in Python. Use `find()` to search from the left.

---

### `index(sub)`
Returns the **index of the first occurrence** of a substring.
**Raises a `ValueError`** if the substring is not found (unlike `find()` which returns -1).

**Where to use:** When you are sure the substring exists and want an error if it doesn't (safer in critical code).

```python
sentence = "python is fun and python is powerful"
print(sentence.index("fun"))    # Output: 10

# When substring is NOT found — raises an error
try:
    print(sentence.index("java"))
except ValueError:
    print("Substring not found!")  # Output: Substring not found!
```

> **`find()` vs `index()`**
> | | `find()` | `index()` |
> |---|---|---|
> | Not found | Returns `-1` | Raises `ValueError` |
> | Safe to use? | Yes, always | Only when sure it exists |

---

### `startswith(prefix)`
Returns `True` if the string **starts with** the given prefix, otherwise `False`.

**Where to use:** Validating URLs (starts with "https"), checking file extensions, filtering data.

```python
sentence = "python is fun and python is powerful"
print(sentence.startswith("p"))        # Output: True
print(sentence.startswith("python"))   # Output: True
print(sentence.startswith("Java"))     # Output: False

url = "https://github.com"
print(url.startswith("https"))         # Output: True
```

---

### `endswith(suffix)`
Returns `True` if the string **ends with** the given suffix, otherwise `False`.

**Where to use:** Checking file extensions, validating endings of strings.

```python
sentence = "python is fun and python is powerful"
print(sentence.endswith("r"))           # Output: False
print(sentence.endswith("powerful"))    # Output: True

filename = "notes.py"
print(filename.endswith(".py"))         # Output: True
print(filename.endswith(".txt"))        # Output: False
```

---

### `isalpha()`
Returns `True` if **all characters are alphabets** (A–Z, a–z) and the string is not empty.

**Where to use:** Validating names (should contain only letters, no numbers or symbols).

```python
print("Python".isalpha())      # Output: True
print("Python3".isalpha())     # Output: False  (contains a digit)
print("Hello World".isalpha()) # Output: False  (contains a space)

name = input("Enter your name: ")
if name.isalpha():
    print("Valid name!")
else:
    print("Name should contain letters only.")
```

---

### `isdigit()`
Returns `True` if **all characters are digits** (0–9) and the string is not empty.

**Where to use:** Validating if user input is a number before converting with `int()`.

```python
print("12345".isdigit())    # Output: True
print("123.5".isdigit())    # Output: False  (dot is not a digit)
print("123abc".isdigit())   # Output: False  (contains letters)

age = input("Enter your age: ")
if age.isdigit():
    print("Valid age:", int(age))
else:
    print("Please enter numbers only.")
```

---

### `isalnum()`
Returns `True` if the string contains **only letters and numbers** (no spaces or symbols).

**Where to use:** Validating usernames (letters and digits only, no special characters).

```python
print("Python3".isalnum())    # Output: True
print("Aj Kumar".isalnum())   # Output: False  (contains a space)
print("aj@123".isalnum())     # Output: False  (contains @)

username = "AjKumar45"
print(username.isalnum())     # Output: True  (valid username format)
```

---

### `isupper()`
Returns `True` if **all letters** in the string are uppercase.

**Where to use:** Checking if a constant or code is in the expected format.

```python
print("PYTHON".isupper())     # Output: True
print("Python".isupper())     # Output: False
print("PYTHON3".isupper())    # Output: True  (digits are ignored)

code = "AJ001"
print(code.isupper())         # Output: True
```

---

### `islower()`
Returns `True` if **all letters** in the string are lowercase.

**Where to use:** Checking if an email or username is in lowercase format.

```python
print("python".islower())     # Output: True
print("Python".islower())     # Output: False
print("python3".islower())    # Output: True  (digits are ignored)

email = "aj.kumar@gmail.com"
print(email.islower())        # Output: True
```

---

### `center(width, fillchar)`
Centers the string within a given width, padding with the specified fill character (default is space).

**Where to use:** Formatting text output, CLI menus, headers in reports.

```python
print("Python".center(12, "-"))   # Output: ---Python---
print("Python".center(12, "*"))   # Output: ***Python***
print("Python".center(12))        # Output: "   Python   "

# Real use: printing a centered header
print("REPORT".center(30, "="))   # Output: ============REPORT============
```

---

### `max()` with strings
`max()` is a **built-in function** (not a string method). When used on a string or list of strings, it returns the "largest" item based on ASCII/alphabetical value or a custom key.

**Where to use:** Finding the longest word, the alphabetically last word.

```python
# Finding the longest word in a sentence
text = "I love Python programming"
longest_word = max(text.split(), key=len)
print(longest_word)   # Output: programming

# key=len tells max() to compare by length, not alphabetically

# Without key= (compares alphabetically)
words = ["banana", "apple", "cherry"]
print(max(words))           # Output: cherry  (alphabetically last)

# On a list of numbers
numbers = [10, 25, 4]
print(max(numbers))         # Output: 25
```

---

## Chaining Multiple Methods

You can **chain** string methods — they are applied left to right, one after another.

**Where to use:** Cleaning and transforming input in one clean line.

```python
text = '   I am a Python program.   '
result = text.strip().upper().replace("A", "THE")
print(result)
# Output: I TOM THE PYTHON PROGRTHM.

# Step by step:
# 1. text.strip()           → 'I am a Python program.'
# 2. .upper()               → 'I AM A PYTHON PROGRAM.'
# 3. .replace("A", "THE")   → 'I THM THE PYTHON PROGRTHM.'
```

---

## Quick Reference — All String Methods

```python
# CASE METHODS
str.upper()           # All uppercase
str.lower()           # All lowercase
str.swapcase()        # Swap upper/lower
str.capitalize()      # First letter upper, rest lower
str.title()           # First letter of each word upper

# SPACE CLEANING
str.strip()           # Remove spaces from both sides
str.lstrip()          # Remove spaces from left only
str.rstrip()          # Remove spaces from right only

# SEARCH & CHECK
str.find(sub)         # Index of first match, -1 if not found
str.rfind(sub)        # Index of last match, -1 if not found
str.index(sub)        # Index of first match, ValueError if not found
str.count(sub)        # Number of occurrences
str.startswith(pre)   # True if string starts with prefix
str.endswith(suf)     # True if string ends with suffix

# MODIFY
str.replace(old, new) # Replace all occurrences
str.split(sep)        # Split into list (default: whitespace)
str.join(iterable)    # Join list into string

# VALIDATION (return True/False)
str.isalpha()         # Only letters?
str.isdigit()         # Only digits?
str.isalnum()         # Only letters and digits?
str.isupper()         # All uppercase?
str.islower()         # All lowercase?

# FORMATTING
str.center(width, char)   # Center with fill character
len(str)                  # Length of string
max(list, key=len)        # Longest item in list
```
---
#### **2.3 Accessing String Characters:**
You can access individual characters in a string using **indexing**. Python uses zero-based indexing, so the first character has an index of 0.

```python
text = "Python"
print(text[0])  # Output: P
print(text[2])  # Output: t
```

You can also use **negative indexing** to start counting from the end of the string.
```python
print(text[-1])  # Output: n
print(text[-3])  # Output: h
```

#### **2.4 Slicing Strings:**
You can extract a portion (substring) of a string using slicing.

```python
text = "Python Programming"
print(text[0:6])  # Output: Python (extracts from index 0 to 5)
print(text[:6])  # Output: Python (same as above)
print(text[7:])  # Output: Programming (from index 7 to the end)
print(a[:])
print(a[0:6]) 
print(a[0:]) #omitting end
print(a[:6])#omitting start
print(a[::2]) 
print(a[::-1])#reverse a string 
```

---

### **3. Comments in Python**

Comments are ignored by the Python interpreter and are used to explain the code or leave notes for yourself or others. They do not affect the execution of the program.

- **Single-line comments** start with `#`:
  ```python
  # This is a single-line comment
  print("Hello, World!")
  ```

- **Multi-line comments** can be written using triple quotes (`"""` or `'''`). These are often used to write detailed explanations or temporarily block sections of code:
  ```python
  """
  This is a multi-line comment.
  It can span multiple lines.
  """
  print("Hello, Python!")
  ```

---

### **4. Escape Sequences**
Escape sequences are special characters in strings that start with a backslash (`\`). They are used to represent certain special characters.

Some commonly used escape sequences:
- `\n`: New Line         
- `\t`': Tab Space
- `\\`: Backslash
#### **Example:**
```python
print("Hello\nWorld")  # Output: 
# Hello
# World

print("Hello\tPython")  # Output: Hello    Python
```

---
