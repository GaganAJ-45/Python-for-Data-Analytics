# File Handling in Python
> Foundation Notes — Interview Ready | DSA Focused

---

## 1. What is File Handling?

File handling allows Python programs to **read from and write to files** on disk. This is essential for data persistence — saving data that survives after the program ends.

```
Program (RAM)  ←→  File Handling  ←→  File (Disk)
```

**Why file handling matters for your roles:**
- Data Analytics — reading CSV, JSON datasets
- Python Engineering — config files, logs, data pipelines
- Software Dev — storing and retrieving application data

---

## 2. Opening a File — `open()`

```python
file = open("filename.txt", mode)
```

### File Modes

| Mode | Meaning | File exists? | File missing? |
|---|---|---|---|
| `"r"` | Read (default) | Reads from start | ❌ FileNotFoundError |
| `"w"` | Write | Overwrites completely | Creates new file |
| `"a"` | Append | Adds to end | Creates new file |
| `"x"` | Create | ❌ FileExistsError | Creates new file |
| `"r+"` | Read + Write | Reads/writes | ❌ FileNotFoundError |
| `"rb"` | Read binary | Reads bytes | ❌ FileNotFoundError |
| `"wb"` | Write binary | Writes bytes | Creates new file |

```python
# Open for reading
f = open("data.txt", "r")

# Open for writing — creates or overwrites
f = open("data.txt", "w")

# Open for appending — adds to existing content
f = open("data.txt", "a")

# Always close after opening manually
f.close()
```

> ⚠️ **Always close files.** An unclosed file wastes resources and can cause data loss. Use `with` to avoid forgetting — explained next.

---

## 3. `with` Statement — The Pythonic Way

`with` automatically closes the file when the block exits — even if an exception occurs.

```python
# ✅ Pythonic — file closes automatically
with open("data.txt", "r") as f:
    content = f.read()
# file is closed here — no need to call f.close()

# ❌ Manual — easy to forget close
f = open("data.txt", "r")
content = f.read()
f.close()   # what if an exception happens before this?
```

> **Interview tip:** Always use `with open(...)` in interviews. It shows you know Pythonic patterns and understand resource management.

---

## 4. Reading Files

### `read()` — reads entire file as one string
```python
with open("data.txt", "r") as f:
    content = f.read()
    print(content)
```

### `readline()` — reads one line at a time
```python
with open("data.txt", "r") as f:
    line1 = f.readline()   # reads first line
    line2 = f.readline()   # reads second line
    print(line1)
    print(line2)
```

### `readlines()` — reads all lines into a list
```python
with open("data.txt", "r") as f:
    lines = f.readlines()   # ["line1\n", "line2\n", "line3\n"]
    print(lines)

# Strip newline characters
lines = [line.strip() for line in lines]
```

### Iterating line by line — most memory efficient
```python
with open("data.txt", "r") as f:
    for line in f:          # reads one line at a time
        print(line.strip())
```

> **Interview tip:** For large files, always iterate line by line — `readlines()` loads the entire file into memory which fails on large datasets. Line-by-line iteration uses O(1) memory.

---

## 5. Writing Files

### `write()` — writes a string
```python
with open("output.txt", "w") as f:
    f.write("Hello, Python!\n")
    f.write("File handling is useful.\n")
# Creates or overwrites output.txt
```

### `writelines()` — writes a list of strings
```python
lines = ["Line 1\n", "Line 2\n", "Line 3\n"]
with open("output.txt", "w") as f:
    f.writelines(lines)
```

### `append` mode — add without overwriting
```python
with open("log.txt", "a") as f:
    f.write("New log entry\n")   # adds to existing content
```

**Write vs Append comparison:**
```python
# First run
with open("test.txt", "w") as f:
    f.write("First write\n")

# Second run — "w" mode OVERWRITES
with open("test.txt", "w") as f:
    f.write("Second write\n")
# File now contains only "Second write"

# "a" mode APPENDS
with open("test.txt", "a") as f:
    f.write("Appended line\n")
# File now contains both lines
```

---

## 6. File Pointer — `seek()` and `tell()`

```python
with open("data.txt", "r") as f:
    print(f.tell())        # Output: 0 — start of file

    content = f.read(5)    # read 5 characters
    print(f.tell())        # Output: 5 — pointer moved

    f.seek(0)              # move pointer back to start
    content = f.read()     # read from beginning again
```

---

## 7. File and Path Operations — `os` Module

```python
import os

# Check if file exists
print(os.path.exists("data.txt"))      # True or False

# Check if it's a file vs directory
print(os.path.isfile("data.txt"))      # True
print(os.path.isdir("my_folder"))      # True

# Get file size in bytes
print(os.path.getsize("data.txt"))

# Get file name and extension
print(os.path.basename("folder/data.txt"))   # data.txt
print(os.path.splitext("data.txt"))          # ('data', '.txt')

# Current working directory
print(os.getcwd())

# Join paths (works on Windows and Linux)
path = os.path.join("folder", "subfolder", "data.txt")
print(path)   # folder/subfolder/data.txt

# List files in directory
print(os.listdir("."))   # list current directory

# Create a directory
os.makedirs("new_folder", exist_ok=True)   # exist_ok avoids error if exists

# Delete a file
os.remove("old_file.txt")

# Rename a file
os.rename("old.txt", "new.txt")
```

---

## 8. `pathlib` — Modern Path Handling (Python 3.4+)

```python
from pathlib import Path

# Create path object
p = Path("data.txt")

# Check existence
print(p.exists())      # True or False
print(p.is_file())     # True
print(p.is_dir())      # False

# Read and write directly
p.write_text("Hello from pathlib!")
content = p.read_text()
print(content)

# File info
print(p.name)          # data.txt
print(p.stem)          # data
print(p.suffix)        # .txt
print(p.parent)        # . (current directory)

# Join paths with / operator
path = Path("folder") / "subfolder" / "data.txt"
print(path)   # folder/subfolder/data.txt

# List all .txt files in directory
for txt_file in Path(".").glob("*.txt"):
    print(txt_file)
```

> **Interview tip:** `pathlib` is the modern Pythonic way — use it over `os.path` in new code. Interviewers value knowing both.

---

## 9. Exception Handling with Files

```python
def read_file(filename):
    try:
        with open(filename, "r") as f:
            return f.read()
    except FileNotFoundError:
        print(f"Error: '{filename}' not found")
        return None
    except PermissionError:
        print(f"Error: No permission to read '{filename}'")
        return None
    except Exception as e:
        print(f"Unexpected error: {e}")
        return None

content = read_file("data.txt")
if content:
    print(content)
```

```python
def safe_write(filename, content):
    try:
        with open(filename, "w") as f:
            f.write(content)
        print(f"Written to {filename}")
    except PermissionError:
        print("Error: Cannot write — permission denied")
    except IsADirectoryError:
        print("Error: Path is a directory, not a file")
```

---

## 10. CSV Files — `csv` Module

CSV (Comma Separated Values) is the most common format in data analytics.

### Reading CSV
```python
import csv

# Read as list of rows
with open("students.csv", "r") as f:
    reader = csv.reader(f)
    for row in reader:
        print(row)   # each row is a list

# Output for students.csv (Name,Age,Marks):
# ['Name', 'Age', 'Marks']
# ['AJ', '22', '85']
# ['Rahul', '21', '92']
```

### Reading CSV as dictionaries — `DictReader`
```python
import csv

with open("students.csv", "r") as f:
    reader = csv.DictReader(f)    # uses first row as keys
    for row in reader:
        print(row["Name"], row["Marks"])

# Output:
# AJ 85
# Rahul 92
```

### Writing CSV
```python
import csv

data = [
    ["Name", "Age", "Marks"],
    ["AJ", 22, 85],
    ["Rahul", 21, 92],
    ["Priya", 23, 78]
]

with open("students.csv", "w", newline="") as f:
    writer = csv.writer(f)
    writer.writerows(data)
```

### Writing CSV with DictWriter
```python
import csv

students = [
    {"Name": "AJ",    "Age": 22, "Marks": 85},
    {"Name": "Rahul", "Age": 21, "Marks": 92},
]

with open("students.csv", "w", newline="") as f:
    fieldnames = ["Name", "Age", "Marks"]
    writer = csv.DictWriter(f, fieldnames=fieldnames)
    writer.writeheader()       # writes Name,Age,Marks
    writer.writerows(students)
```

> **Interview tip:** Always use `newline=""` when opening CSV files for writing on Windows — otherwise Python adds extra blank lines between rows.

---

## 11. JSON Files — `json` Module

JSON (JavaScript Object Notation) is used everywhere — APIs, configs, data storage.

### Writing JSON — `json.dump()`
```python
import json

data = {
    "name": "AJ",
    "age": 22,
    "skills": ["Python", "SQL", "Data Analytics"],
    "scores": {"math": 90, "python": 95}
}

with open("profile.json", "w") as f:
    json.dump(data, f, indent=4)   # indent=4 for pretty printing
```

**profile.json output:**
```json
{
    "name": "AJ",
    "age": 22,
    "skills": ["Python", "SQL", "Data Analytics"],
    "scores": {
        "math": 90,
        "python": 95
    }
}
```

### Reading JSON — `json.load()`
```python
import json

with open("profile.json", "r") as f:
    data = json.load(f)   # returns Python dict

print(data["name"])          # Output: AJ
print(data["skills"][0])     # Output: Python
print(data["scores"]["python"])  # Output: 95
```

### JSON string conversion — `dumps()` and `loads()`
```python
import json

# Python dict → JSON string
d = {"name": "AJ", "age": 22}
json_str = json.dumps(d)
print(json_str)          # Output: {"name": "AJ", "age": 22}
print(type(json_str))    # Output: <class 'str'>

# JSON string → Python dict
d2 = json.loads(json_str)
print(d2["name"])        # Output: AJ
print(type(d2))          # Output: <class 'dict'>
```

**JSON ↔ Python type mapping:**
| JSON | Python |
|---|---|
| object `{}` | dict |
| array `[]` | list |
| string `""` | str |
| number | int / float |
| `true` / `false` | `True` / `False` |
| `null` | `None` |

---

## 12. Practical Patterns

### Log Writer
```python
from datetime import datetime

def log(message, filename="app.log"):
    timestamp = datetime.now().strftime("%Y-%m-%d %H:%M:%S")
    with open(filename, "a") as f:
        f.write(f"[{timestamp}] {message}\n")

log("Program started")
log("Processing data...")
log("Program finished")
```

### Count Word Frequency in a File
```python
def word_frequency(filename):
    freq = {}
    try:
        with open(filename, "r") as f:
            for line in f:
                for word in line.lower().split():
                    word = word.strip(".,!?")
                    freq[word] = freq.get(word, 0) + 1
    except FileNotFoundError:
        print(f"{filename} not found")
        return {}
    return freq

freq = word_frequency("story.txt")
# Sort by frequency
for word, count in sorted(freq.items(), key=lambda x: x[1], reverse=True)[:5]:
    print(f"{word}: {count}")
```

### Read Student Data from CSV and Compute Average
```python
import csv

def compute_averages(filename):
    results = []
    with open(filename, "r") as f:
        reader = csv.DictReader(f)
        for row in reader:
            avg = (int(row["Math"]) + int(row["Python"]) + int(row["SQL"])) / 3
            results.append({"name": row["Name"], "average": round(avg, 2)})
    return sorted(results, key=lambda x: x["average"], reverse=True)

top_students = compute_averages("marks.csv")
for s in top_students:
    print(f"{s['name']}: {s['average']}")
```

### Config File — Read settings from JSON
```python
import json
import os

def load_config(path="config.json"):
    if not os.path.exists(path):
        # Default config
        return {"debug": False, "max_retries": 3, "timeout": 30}
    with open(path, "r") as f:
        return json.load(f)

config = load_config()
print(config["timeout"])
```

---

## Quick Reference

```python
# OPEN MODES
open("file", "r")   # read
open("file", "w")   # write (overwrites)
open("file", "a")   # append
open("file", "rb")  # read binary

# WITH STATEMENT — always use this
with open("file.txt", "r") as f:
    content = f.read()       # entire file as string
    lines   = f.readlines()  # list of lines
    line    = f.readline()   # one line
    for line in f:           # memory efficient

with open("file.txt", "w") as f:
    f.write("text\n")
    f.writelines(["l1\n", "l2\n"])

# OS MODULE
import os
os.path.exists("file")
os.path.isfile("file")
os.path.getsize("file")
os.path.join("a", "b", "c")
os.getcwd()
os.listdir(".")
os.makedirs("dir", exist_ok=True)
os.remove("file")
os.rename("old", "new")

# PATHLIB
from pathlib import Path
p = Path("file.txt")
p.exists() / p.is_file() / p.read_text() / p.write_text()
Path("a") / "b" / "c"    # join with /

# CSV
import csv
with open("f.csv", "r") as f:
    for row in csv.reader(f): ...
    for row in csv.DictReader(f): row["col"]

with open("f.csv", "w", newline="") as f:
    csv.writer(f).writerows(data)

# JSON
import json
json.dump(obj, f, indent=4)      # write to file
data = json.load(f)              # read from file
json.dumps(obj)                  # dict → string
json.loads(s)                    # string → dict
```

---

## Interview Short Answers

**Q: What is the difference between `read()`, `readline()`, and `readlines()`?**
> `read()` reads the entire file as one single string. `readline()` reads one line at a time — each call advances to the next line. `readlines()` reads all lines and returns them as a list of strings with newline characters included. For large files, iterating line by line with a `for` loop is most memory efficient — it reads one line at a time without loading the whole file.

**Q: What is the difference between `"w"` and `"a"` mode?**
> `"w"` (write) mode opens the file and overwrites all existing content — the file starts empty. If the file doesn't exist, it creates one. `"a"` (append) mode keeps all existing content and adds new content at the end. Use `"w"` when replacing data and `"a"` for logs, audit trails, or any situation where you want to preserve existing data.

**Q: Why should you use `with open()` instead of `open()` directly?**
> `with open()` is a context manager that automatically calls `file.close()` when the block exits — whether normally or due to an exception. Without it, if an exception occurs between `open()` and `close()`, the file stays open, wasting system resources and potentially causing data corruption or locking issues. `with` guarantees the file is always properly closed.

**Q: What is the difference between `json.dump()` and `json.dumps()`?**
> `json.dump(obj, file)` writes JSON directly to a file object. `json.dumps(obj)` (dump to string) converts a Python object to a JSON-formatted string in memory. Similarly, `json.load(file)` reads JSON from a file, and `json.loads(string)` parses a JSON string. The `s` suffix always means "string".

**Q: How do you handle a file that may or may not exist?**
> The safest way is to use try-except with `FileNotFoundError`, or check first with `os.path.exists()` or `Path.exists()`. The try-except approach is preferred in Python — it follows the EAFP principle (Easier to Ask Forgiveness than Permission) vs LBYL (Look Before You Leap). For writing, using `"a"` or `"w"` mode automatically creates the file if it doesn't exist.

**Q: What is the difference between `os.path` and `pathlib`?**
> `os.path` is the older, function-based approach — you call functions like `os.path.join()`, `os.path.exists()`. `pathlib` (Python 3.4+) is the modern object-oriented approach — you create `Path` objects and call methods on them. `pathlib` is more readable, supports the `/` operator for joining paths, and handles platform differences (Windows vs Linux) automatically. New code should use `pathlib`.

**Q: Why is `newline=""` needed when writing CSV files?**
> On Windows, Python's universal newline mode translates `\n` to `\r\n`. The `csv` module already adds its own line terminators, so without `newline=""`, each row gets `\r\r\n` — adding an extra blank line between every row. Passing `newline=""` disables Python's newline translation and lets the csv module control line endings directly.
