# 🔢 NumPy — Numerical Python

> **NumPy** (Numerical Python) is the foundational library for **numerical computing** in Python. It provides fast arrays, mathematical operations, and vectorized computations that power modern data science, machine learning, and AI.


## 📦 Installation

```bash
pip install numpy
```

```python
import numpy as np
```

## 📌 Table of Contents

1. [Why NumPy?](#-why-numpy)
2. [Array Dimensions & Ranks](#-array-dimensions--ranks)
3. [2D Arrays (Matrix)](#1-two-dimensional-2d-arrays)
4. [3D Arrays](#2-three-dimensional-3d-arrays)
5. [Array Slicing](#3-array-slicing)
6. [Slicing of 2D Arrays](#4-slicing-of-2d-arrays-matrix)
7. [Advanced Slicing Techniques](#5-advanced-slicing-techniques)
8. [Scalar Arithmetic](#6-scalar-arithmetic)
9. [Vectorized Math Functions](#8-vectorized-math-functions)
10. [Element-Wise Operations](#9-element-wise-operations)
11. [Comparison Operations](#10-comparison-operations)
12. [Broadcasting](#11-broadcasting-in-numpy)
13. [Aggregate Functions](#12-aggregate-functions)
14. [Boolean Filtering](#13-boolean-filtering)


## 🚀 Why NumPy?

### The Problem with Python Lists
Python lists are **slow for large data**. They are general-purpose and not optimized for numerical work.

### NumPy Arrays Are:
- ⚡ **Faster** than Python lists
- 🧠 **Memory Efficient**
- 🔗 **Used internally by Pandas**, scikit-learn, TensorFlow, and more

### NumPy Provides:
- ✅ Fast arrays
- ✅ Mathematical operations
- ✅ Vectorized computations

### Why Python + NumPy is Dominant in AI/ML:
Python is very famous for AI, ML, and data science because:
- It has a rich **ecosystem of libraries**
- It is **easy to write** and read
- It **integrates well** with modern technologies like APIs, DBs, and web apps
- This makes Python very easy for **building and deploying real-world AI tools**



## 📐 Array Dimensions & Ranks

In NumPy, the number of dimensions in an array is referred to as its **rank**.

| Rank | Description | Analogy |
|------|-------------|---------|
| 1D   | Single list of values | A row of data |
| 2D   | Rows and columns | A spreadsheet / table |
| 3D   | Collection of 2D tables | Layers of tables stacked together |



## 1. Two Dimensional (2D) Arrays

A **2D array** represents a **matrix**. It considers both rows and columns. In code, you create it by **nesting a list within a list**.

```python
import numpy as np

array_2d = np.array([['A', 'B', 'C'],
                     ['D', 'E', 'F'],
                     ['G', 'H', 'I']])

print(array_2d.ndim)              # Number of dimensions → 2
print(array_2d.shape)             # Shape → (3, 3)
print(array_2d.size)              # Total elements → 9
print(array_2d[row_index][col_index])  # Access specific element
```


## 2. Three Dimensional (3D) Arrays

A **3D array** adds a third dimension called the **depth** or **layer**. In code, create it by nesting a 2D array inside another list.

```python
import numpy as np

array_3d = np.array([[[1, 2], [3, 4]],
                     [[5, 6], [7, 8]]])

print(array_3d[0, 0, 0])   # Access first element
print(array_3d[1][0][1])   # Alternate access style
```



## 3. Array Slicing

**Slicing** is the process of extracting a specific portion of an array **without copying** the entire dataset.

This is done using the **subscript operator** `[ ]` and the **colon** `:`.

### Syntax:
```python
array[start : end : step]
```

| Parameter | Description |
|-----------|-------------|
| `start`   | Starting index (inclusive) |
| `end`     | Ending index (exclusive) |
| `step`    | Step size to skip elements |

---

## 4. Slicing of 2D Arrays (Matrix)

When working with a 2D array, you can slice by **rows**, **columns**, and **blocks of data**.

### 🔹 Row Selection

```python
# Single row — only one specific row
array[1]        # Returns row at index 1

# Range of rows — returns rows 0, 1, 2 (3 is exclusive)
array[0:3]

# Every specific row — step 2, skips every other row
array[0:4:2]
```

### 🔹 Column Selection

To slice columns, you must use a **comma** to separate the rows and columns selection.

```python
# Single column — all rows, column at index 0
array[0:3, 0]

# Range of columns — all rows, columns 0 to 2
array[0:3, 0:3]
```

---

## 5. Advanced Slicing Techniques

### 🔹 Negative Indexing
Use negative values to access elements **from the end** of the array.

```python
array[-1]    # Very last row
```

### 🔹 Reversing
The order of rows or columns can be reversed by using a **step of `-1`**.

```python
# Reverse the row order
array[0:3, ::-1]

# Reverse the column order
array[0:3, 0:4:-1]
```

---

## 6. Scalar Arithmetic

In NumPy, **scalar arithmetic** refers to performing mathematical operations between an **array** and a **single numerical value**.

When you apply operations like `+`, `-`, `*`, `/`, `**` to an array using a scalar, NumPy applies it to **every individual element** in the array.

This is a core concept called **Vectorization** — it allows you to **avoid writing for loops** in Python.

```python
array1d = np.array([1, 2, 3, 4])
print(array1d * 1)    # Multiplies every element by 1
```

### ✅ Why Use Scalar Arithmetic?

| Reason | Benefit |
|--------|---------|
| **Readability** | Cleaner, shorter code |
| **Speed** | Much faster than Python loops |
| **Consistency** | Uniform operation on all elements |

---

## 8. Vectorized Math Functions

NumPy allows you to perform **mathematical operations or functions on an entire array at once**, without the need of writing for loops.

- You can access functions directly through the **NumPy library** (`imported as np`)
- When you pass an array into these functions, it is written into the new function where it is applied

```python
print(np.sqrt(array))      # Square root of each element
print(np.round(array))     # Round each element
print(np.sin(array))       # Sine of each element
```

### 📌 NumPy Constants
NumPy also provides mathematical constants:

```python
np.pi    # π = 3.14159...
np.e     # e = 2.71828...
```

---

## 9. Element-Wise Operations

Element-wise operations apply an operation to **each corresponding element** between two arrays of the same shape.

```python
array1 = np.array([1, 2, 3])
array2 = np.array([4, 5, 6])

print(array1 + array2)
# Output: [5, 7, 9]
```

---

## 10. Comparison Operations

NumPy allows you to **compare every element** in an array against:
- A **value (scalar)**
- **Another array**

NumPy returns a **Boolean array** containing `True` or `False` for each element.

```python
array = np.array([10, 20, 30, 40])
print(array > 15)
# Output: [False  True  True  True]
```

---

## 11. Broadcasting in NumPy

**Broadcasting** is a powerful mechanism in NumPy that allows arithmetic operations between arrays of **different shapes**.

### Rules for Broadcasting:
For two arrays to be **compatible**, their dimensions must follow these rules when compared from **right → left**:

1. The dimensions are **equal**, OR
2. One of the dimensions is **1**

```
Example:
(2, 1)  +  (1, 4)  →  (2, 4)   ✅ Compatible
(4, 1)  +  (1, 1)  →  (4, 1)   ✅ Compatible
```

```python
import numpy as np
#broadcating in numpy
array1d = np.array([[1,2,3,4,5,6]])
array1 = np.array([[7],[8],[9],[10],[11],[12]])
print(array1d.shape)
print(array1.shape)

print(array1d + array1)
```

#### output
```
(1, 6)
(6, 1)
[[ 8  9 10 11 12 13]
 [ 9 10 11 12 13 14]
 [10 11 12 13 14 15]
 [11 12 13 14 15 16]
 [12 13 14 15 16 17]
 [13 14 15 16 17 18]]
```

---

## 12. Aggregate Functions

Aggregate functions **summarize the entire array** and result in **one value**. Their power comes from the ability to perform calculations along **specific axes**.

| Axis | Behaviour |
|------|-----------|
| `axis=0` | Collapses the entire **row** to perform the calculation for each **column** |
| `axis=1` | Collapses the entire **column** to perform the calculation for each **row** |

```python
array = np.array([[1, 2, 3],
                  [4, 5, 6]])

np.sum(array, axis=0)   # Sum of each column → [5, 7, 9]
np.sum(array, axis=1)   # Sum of each row   → [6, 15]
np.mean(array)          # Overall mean
np.max(array)           # Maximum value
np.min(array)           # Minimum value
```

---

## 13. Boolean Filtering

**Filtering in NumPy** is the process of **selecting specific elements** from an array that meet a condition, and creating a **new array** from them.

### Two Main Ways to Filter:
1. **Boolean Indexing** — `array[condition]`
2. **`np.where()` function**

---

### 🔹 Boolean Indexing

This is the **most common method**. Pass the comparison condition directly into the array's brackets. NumPy checks every element and **only keeps the ones that are `True`**.

```python
ages = np.array([12, 15, 17, 20, 25])
teenagers = ages[ages < 18]
print(teenagers)
# Output: [12, 15, 17]
```

You can also use **logical operators** like `&` (and), `|` (or):

```python
result = ages[(ages >= 13) & (ages < 18)]
```

---

### 🔹 `np.where()` Function (Preserve Shape / Replace)

Use `np.where()` when you want to **preserve the original array's shape** and simply **replace elements** that don't match the condition with a **placeholder** (like `0`).

```python
np.where(condition, value_if_true, value_if_false)
```

```python
ages = np.array([12, 15, 20, 25])
result = np.where(ages < 18, ages, 0)
# Output: [12, 15,  0,  0]
```

---

## 🗂️ Quick Reference Cheat Sheet

```python
import numpy as np

# --- Array Creation ---
arr = np.array([1, 2, 3])
arr_2d = np.array([[1, 2], [3, 4]])

# --- Array Info ---
arr.ndim       # Number of dimensions
arr.shape      # Shape (rows, cols)
arr.size       # Total number of elements

# --- Slicing ---
arr[1:4]       # Elements index 1 to 3
arr[::2]       # Every 2nd element
arr[::-1]      # Reversed

# --- Math ---
arr + 10       # Add 10 to all elements
arr * 2        # Multiply all by 2
arr ** 2       # Square all elements

# --- Math Functions ---
np.sqrt(arr)
np.sin(arr)
np.round(arr)

# --- Aggregate ---
np.sum(arr)
np.mean(arr)
np.max(arr)
np.min(arr)

# --- Boolean Filtering ---
arr[arr > 2]
np.where(arr > 2, arr, 0)

# --- Constants ---
np.pi          # 3.14159...
np.e           # 2.71828...
```

---

## 🌍 Where is NumPy Used?

NumPy is widely used in fields that involve data processing:

- 🤖 **Machine Learning** — arrays for model inputs/outputs
- 📊 **Data Science** — data manipulation and analysis
- 🧠 **Artificial Intelligence** — matrix operations in neural networks
- 📈 **Finance** — numerical computations on large datasets
- 🔬 **Scientific Research** — simulations and computations


<div align="center">

📝 *Notes compiled from handwritten study material*  
🚀 *Happy Learning NumPy!*

</div>
