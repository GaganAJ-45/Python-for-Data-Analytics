# Python Generators in Python

## Table of Contents

1. [Introduction to Generators](#1-introduction-to-generators)
2. [Understanding `return` vs `yield`](#2-understanding-return-vs-yield)
3. [Generator Functions](#3-generator-functions)
4. [Generator Objects](#4-generator-objects)
5. [Understanding `next()`](#5-understanding-next)
6. [StopIteration Exception](#6-stopiteration-exception)
7. [Iterable vs Iterator](#7-iterable-vs-iterator)
8. [Iterator vs Generator](#8-iterator-vs-generator)
9. [Why Do We Need Generators?](#9-why-do-we-need-generators)
10. [Generator Expressions](#10-generator-expressions)
11. [Generator Expressions with Conditions](#11-generator-expressions-with-conditions)
12. [Generator Functions with Parameters](#12-generator-functions-with-parameters)
13. [`yield` vs `yield from`](#13-yield-vs-yield-from)
14. [Lazy Evaluation](#14-lazy-evaluation)
15. [Iterator Protocol](#15-iterator-protocol)
16. [Generator Exhaustion](#16-generator-exhaustion)
17. [Generator vs List Comprehension](#17-generator-vs-list-comprehension)
18. [Real-Time Applications of Generators](#18-real-time-applications-of-generators)
19. [Important Interview Questions](#19-important-interview-questions)

---

# 1. Introduction to Generators

### Definition

A **Generator** is a special type of iterator in Python that produces values one at a time instead of storing all values in memory.

Generators use the `yield` keyword to produce values.

### Why do we need Generators?

Consider a situation where we need to generate a large number of values.

Using a normal list, Python stores all the generated values in memory.

Using a generator, Python produces values only when they are requested.

**Main advantages:**
- Memory efficiency.
- Lazy evaluation.
- Values are generated one at a time.
- Useful for processing large datasets.
- Suitable for data streams and large files.

---

# 2. Understanding `return` vs `yield`

Before understanding generators, we need to understand the difference between `return` and `yield`.

## 2.1 What is `return`?

### Definition

The `return` keyword sends a value back to the caller and immediately terminates the function.

### Example

```python
def numbers():
    print("Start")

    return 10

    print("End")


result = numbers()

print(result)
```

**Output:**

```text
Start
10
```

### Explanation

1. Function execution starts.
2. Prints `Start`.
3. `return 10` sends the value 10 to the caller.
4. The function terminates.
5. `print("End")` will not execute.

## 2.2 What is `yield`?

### Definition

`yield` is a Python keyword that produces a value and temporarily pauses the execution of a generator function.

The function can resume execution from where it was paused.

### Example

```python
def numbers():
    print("Start")

    yield 10

    print("End")

    yield 20


result = numbers()

print(next(result))
print(next(result))
```

**Output:**

```text
Start
10
End
20
```

### Explanation

1. First `next()` starts the function.
2. Prints `Start`.
3. `yield 10` produces 10 and pauses execution.
4. Second `next()` resumes execution.
5. Prints `End`.
6. `yield 20` produces 20 and pauses execution.

## 2.3 Difference between `return` and `yield`

| `return` | `yield` |
|---|---|
| Returns a value to the caller. | Produces a value to the caller. |
| Terminates the function. | Temporarily pauses the function. |
| Cannot resume execution after returning. | Can resume execution from the paused position. |
| Does not create a generator by itself. | Makes the function a generator function. |
| Used in normal functions. | Used in generator functions. |

---

# 3. Generator Functions

### Definition

A **Generator Function** is a special type of Python function that contains the `yield` keyword and produces a sequence of values one at a time.

### Syntax

```python
def function_name():
    yield value1
    yield value2
    yield value3
```

### Example

```python
def numbers():
    yield 10
    yield 20
    yield 30


result = numbers()

for num in result:
    print(num)
```

**Output:**

```text
10
20
30
```

### Important Points

- Generator functions are defined using the `def` keyword.
- They use `yield` to produce values.
- Calling a generator function creates a generator object.
- The function body does not execute immediately.
- Execution starts when values are requested.

---

# 4. Generator Objects

### Definition

A **Generator Object** is an iterator created when a generator function is called.

It maintains the function's execution state and produces values when requested.

### Example

```python
def numbers():
    print("Start")

    yield 10
    yield 20
    yield 30


result = numbers()

print(result)
```

**Output:**

```text
<generator object numbers at ...>
```

### Why does it print a generator object?

When we execute:

```python
result = numbers()
```

Python does not execute the function body immediately.

Instead, it creates a generator object.

The function starts executing only when we request a value using `next()` or iterate over the generator.

---

# 5. Understanding `next()`

### Definition

`next()` is a built-in Python function that retrieves the next available value from an iterator or generator.

### Syntax

```python
next(iterator)
```

### Example

```python
def numbers():
    yield 10
    yield 20
    yield 30


result = numbers()

print(next(result))
print(next(result))
print(next(result))
```

**Output:**

```text
10
20
30
```

### Execution Flow

| Step | Execution | Result |
|---|---|---|
| 1 | `result = numbers()` | Creates generator object. |
| 2 | `next(result)` | Produces 10. |
| 3 | `next(result)` | Produces 20. |
| 4 | `next(result)` | Produces 30. |

### Important Point

Every time `next()` is called:

1. Generator execution starts or resumes.
2. Python executes until it reaches the next `yield`.
3. The yielded value is returned.
4. The generator pauses and preserves its execution state.

---

# 6. StopIteration Exception

### Definition

`StopIteration` is a built-in exception raised when an iterator or generator has no more values to produce.

### Example

```python
def numbers():
    yield 10
    yield 20
    yield 30


result = numbers()

print(next(result))
print(next(result))
print(next(result))
print(next(result))
```

**Output:**

```text
10
20
30

StopIteration
```

### Why does StopIteration occur?

Our generator contains only three `yield` statements.

After producing the third value, the generator finishes execution.

When we call `next()` again, Python raises `StopIteration`.

### Handling StopIteration

We can handle this exception using `try-except`.

```python
def numbers():
    yield 10
    yield 20
    yield 30


result = numbers()

try:
    print(next(result))
    print(next(result))
    print(next(result))
    print(next(result))

except StopIteration:
    print("Generator is exhausted")
```

**Output:**

```text
10
20
30
Generator is exhausted
```

---

# 7. Iterable vs Iterator

## 7.1 What is an Iterable?

### Definition

An **Iterable** is an object that can return an iterator using the `iter()` function.

Examples:
- List
- Tuple
- String
- Set
- Dictionary

### Example

```python
numbers = [10, 20, 30]

result = iter(numbers)

print(type(numbers))
print(type(result))
```

**Output:**

```text
<class 'list'>
<class 'list_iterator'>
```

Here:
- `numbers` is an iterable.
- `result` is an iterator.

## 7.2 What is an Iterator?

### Definition

An **Iterator** is an object that allows us to access elements one at a time and maintains its current iteration state.

Python provides two important functions:

- `iter()` – Obtains an iterator.
- `next()` – Retrieves the next element.

### Example

```python
numbers = [10, 20, 30, 40]

result = iter(numbers)

print(next(result))
print(next(result))
print(next(result))
print(next(result))
```

**Output:**

```text
10
20
30
40
```

### Difference between Iterable and Iterator

| Iterable | Iterator |
|---|---|
| An object that can be iterated over. | An object that provides elements one at a time. |
| Can provide an iterator using `iter()`. | Retrieves elements using `next()`. |
| Examples: List, Tuple, String. | Examples: List Iterator, Generator Object. |
| Can generally create multiple iterators. | Maintains its current iteration position. |

---

# 8. Iterator vs Generator

### Iterator

An iterator is an object that provides elements one at a time using the iterator protocol.

### Generator

A generator is a special type of iterator that produces values using `yield`.

### Example: Iterator

```python
numbers = [10, 20, 30]

result = iter(numbers)

print(next(result))
print(next(result))
```

**Output:**

```text
10
20
```

### Example: Generator

```python
def numbers():
    yield 10
    yield 20
    yield 30


result = numbers()

print(next(result))
print(next(result))
```

**Output:**

```text
10
20
```

### Difference between Iterator and Generator

| Iterator | Generator |
|---|---|
| An object used to retrieve elements one at a time. | A special type of iterator. |
| Can be created using `iter()` or a custom iterator class. | Can be created using `yield` or a generator expression. |
| Custom implementation may require `__iter__()` and `__next__()`. | Python automatically implements the iterator protocol. |
| Can be implemented using a class. | Can be implemented using a function. |
| Uses `next()` to retrieve values. | Uses `next()` to retrieve values. |

**Important Interview Point:**

Every generator is an iterator, but every iterator is not a generator.

---

# 9. Why Do We Need Generators?

Generators are useful when we want to produce values without storing all of them in memory.

Consider generating numbers from 1 to 1,000,000.

## 9.1 Using a List

```python
def numbers():
    result = []

    for i in range(1, 1000001):
        result.append(i)

    return result


data = numbers()
```

### Explanation

1. Creates an empty list.
2. Generates all numbers.
3. Stores all numbers in the list.
4. Returns the complete list.

All one million integers are stored in memory.

## 9.2 Using a Generator

```python
def numbers():
    for i in range(1, 1000001):
        yield i


data = numbers()

print(next(data))
print(next(data))
print(next(data))
```

**Output:**

```text
1
2
3
```

### Explanation

1. Python creates a generator object.
2. First `next()` generates 1.
3. Second `next()` generates 2.
4. Third `next()` generates 3.

The generator produces values incrementally instead of creating a list containing all values.

### List vs Generator

| List | Generator |
|---|---|
| Stores all elements in memory. | Generates elements when requested. |
| Eager evaluation. | Lazy evaluation. |
| All elements are created upfront. | Elements are produced incrementally. |
| Supports indexing. | Does not support direct indexing. |
| Can be iterated multiple times. | Normally can be consumed only once. |
| Generally requires more memory for large collections. | Generally requires less memory for large sequences. |

**Important:** Generators are not always better than lists. Lists are useful when we need indexing, repeated access, or the complete collection.

---

# 10. Generator Expressions

### Definition

A **Generator Expression** is a compact way to create a generator object without defining a separate generator function using `def` and `yield`.

### Syntax

```python
(variable_expression for variable in iterable)
```

### Example 1: List Comprehension

```python
numbers = [i * 2 for i in range(1, 6)]

print(numbers)
```

**Output:**

```text
[2, 4, 6, 8, 10]
```

Here, Python creates a list containing all values.

### Example 2: Generator Expression

```python
numbers = (i * 2 for i in range(1, 6))

print(numbers)
```

**Output:**

```text
<generator object <genexpr> at ...>
```

Here, Python creates a generator object.

### Retrieving Values

```python
numbers = (i * 2 for i in range(1, 6))

print(next(numbers))
print(next(numbers))
print(next(numbers))
print(next(numbers))
print(next(numbers))
```

**Output:**

```text
2
4
6
8
10
```

### Using a For Loop

```python
numbers = (i * 2 for i in range(1, 6))

for num in numbers:
    print(num)
```

**Output:**

```text
2
4
6
8
10
```

The `for` loop automatically retrieves the next value until the generator is exhausted.

---

# 11. Generator Expressions with Conditions

We can use conditional statements inside generator expressions to filter values.

### Syntax

```python
(variable for variable in iterable if condition)
```

## Example 1: Generate Even Numbers

```python
even_numbers = (i for i in range(1, 11) if i % 2 == 0)

for num in even_numbers:
    print(num)
```

**Output:**

```text
2
4
6
8
10
```

### Explanation

- `range(1, 11)` generates numbers from 1 to 10.
- `if i % 2 == 0` checks whether a number is even.
- Only matching numbers are produced.

## Example 2: Generate Numbers Greater Than 5

```python
numbers = (i for i in range(1, 11) if i > 5)

for num in numbers:
    print(num)
```

**Output:**

```text
6
7
8
9
10
```

## Example 3: Filter Student Marks

```python
marks = [35, 80, 45, 90, 60, 30, 75]

passed_students = (mark for mark in marks if mark >= 50)

for mark in passed_students:
    print(mark)
```

**Output:**

```text
80
90
60
75
```

---

# 12. Generator Functions with Parameters

### Definition

Parameters allow us to pass information into a generator function so that it can produce values dynamically based on the supplied arguments.

### Syntax

```python
def generator_name(parameter):
    yield value
```

## Example 1: Generate Numbers Based on User Input

```python
def numbers(n):
    for i in range(1, n + 1):
        yield i


result = numbers(5)

for num in result:
    print(num)
```

**Output:**

```text
1
2
3
4
5
```

### Explanation

- `n` is the parameter.
- `5` is the argument.
- The generator generates numbers from 1 to 5.
- `yield` produces one value at a time.

## Example 2: Generate Squares

```python
def squares(n):
    for i in range(1, n + 1):
        yield i ** 2


result = squares(5)

for num in result:
    print(num)
```

**Output:**

```text
1
4
9
16
25
```

## Example 3: Multiplication Table

```python
def multiplication(num):
    for i in range(1, 11):
        yield f"{num} * {i} = {num * i}"


multi = multiplication(2)

for value in multi:
    print(value)
```

**Output:**

```text
2 * 1 = 2
2 * 2 = 4
2 * 3 = 6
2 * 4 = 8
2 * 5 = 10
2 * 6 = 12
2 * 7 = 14
2 * 8 = 16
2 * 9 = 18
2 * 10 = 20
```

---

# 13. `yield` vs `yield from`

## 13.1 What is `yield from`?

### Definition

`yield from` is a Python keyword that delegates the production of values to another iterable or generator.

Instead of manually iterating over another iterable and yielding each value, we can use `yield from`.

### Example 1: Using `yield`

```python
def numbers():
    for i in [10, 20, 30, 40]:
        yield i


result = numbers()

for value in result:
    print(value)
```

**Output:**

```text
10
20
30
40
```

### Example 2: Using `yield from`

```python
def numbers():
    yield from [10, 20, 30, 40]


result = numbers()

for value in result:
    print(value)
```

**Output:**

```text
10
20
30
40
```

Both examples produce the same sequence of values.

## Example 3: Delegating to Another Generator

```python
def first():
    yield 10
    yield 20


def second():
    yield 30
    yield 40


def combined():
    yield from first()
    yield from second()


result = combined()

for num in result:
    print(num)
```

**Output:**

```text
10
20
30
40
```

### Difference between `yield` and `yield from`

| `yield` | `yield from` |
|---|---|
| Produces a value. | Delegates value production to another iterable or generator. |
| Used to produce individual values. | Used to produce values from another iterable or generator. |
| Can yield lists as a single value. | Iterates through an iterable and produces its elements individually. |

**Important Example:**

```python
def first():
    yield [10, 20, 30]


def second():
    yield from [10, 20, 30]
```

- `first()` produces one value: the entire list.
- `second()` produces three values: 10, 20, and 30.

---

# 14. Lazy Evaluation

### Definition

**Lazy Evaluation** is an approach in which values are calculated only when they are actually required instead of calculating everything immediately.

Generators use lazy evaluation.

## Example 1: Eager Evaluation Using a List

```python
def numbers():
    result = [i * 2 for i in range(1, 6)]
    return result


data = numbers()

print(data)
```

**Output:**

```text
[2, 4, 6, 8, 10]
```

All values are calculated when the function executes.

## Example 2: Lazy Evaluation Using a Generator

```python
def numbers():
    for i in range(1, 6):
        print("Generating value")
        yield i * 2


result = numbers()

print("Generator created")

print(next(result))
print(next(result))
```

**Output:**

```text
Generator created
Generating value
2
Generating value
4
```

### Explanation

1. `numbers()` creates a generator object.
2. The function body is not executed immediately.
3. First `next()` calculates the first value.
4. Second `next()` calculates the second value.
5. Remaining values are not calculated yet.

### Eager vs Lazy Evaluation

| Eager Evaluation | Lazy Evaluation |
|---|---|
| Calculates values immediately. | Calculates values when requested. |
| All results are created upfront. | Results are produced incrementally. |
| Example: List Comprehension. | Example: Generator Expression. |

---

# 15. Iterator Protocol

### Definition

The **Iterator Protocol** is a set of methods that Python objects must implement to behave as iterators.

It consists of two important methods:

1. `__iter__()`
2. `__next__()`

## 15.1 `__iter__()`

### Definition

`__iter__()` returns an iterator object.

### Example

```python
numbers = [10, 20, 30]

result = numbers.__iter__()

print(type(result))
```

**Output:**

```text
<class 'list_iterator'>
```

We normally use the built-in `iter()` function:

```python
result = iter(numbers)
```

Both approaches obtain an iterator.

## 15.2 `__next__()`

### Definition

`__next__()` returns the next element from an iterator.

When no elements remain, it raises `StopIteration`.

### Example

```python
numbers = [10, 20, 30]

result = iter(numbers)

print(result.__next__())
print(result.__next__())
print(result.__next__())
```

**Output:**

```text
10
20
30
```

We normally use:

```python
next(result)
```

Internally, `next(result)` invokes `result.__next__()`.

## 15.3 How Generators Follow the Iterator Protocol

Generator objects automatically implement both `__iter__()` and `__next__()`.

### Example

```python
def numbers():
    yield 10
    yield 20
    yield 30


result = numbers()

print(iter(result) is result)

print(next(result))
```

**Output:**

```text
True
10
```

### Difference between `__iter__()` and `__next__()`

| `__iter__()` | `__next__()` |
|---|---|
| Returns an iterator. | Returns the next element. |
| Used by `iter()`. | Used by `next()`. |
| Provides access to the iterator. | Advances the iterator. |

---

# 16. Generator Exhaustion

### Definition

**Generator Exhaustion** occurs when a generator has produced all its available values and its execution has completed.

After exhaustion, the generator cannot be restarted.

## Example

```python
def numbers():
    yield 10
    yield 20
    yield 30


result = numbers()

for num in result:
    print(num)


print(list(result))
```

**Output:**

```text
10
20
30
[]
```

### Why does the second list return empty?

1. First, the `for` loop consumes all generator values.
2. The generator reaches the end of its execution.
3. The generator becomes exhausted.
4. The second `list(result)` receives no values.

## Can We Reuse an Exhausted Generator?

No. An exhausted generator cannot be restarted.

However, we can create a new generator object by calling the generator function again.

### Example

```python
def numbers():
    yield 10
    yield 20
    yield 30


result = numbers()

print(list(result))

result = numbers()

print(list(result))
```

**Output:**

```text
[10, 20, 30]
[10, 20, 30]
```

Each call to `numbers()` creates a new generator object.

---

# 17. Generator vs List Comprehension

## 17.1 What is List Comprehension?

### Definition

List Comprehension is a concise way to create a list using a single expression.

### Example

```python
numbers = [i * 2 for i in range(1, 6)]

print(numbers)
```

**Output:**

```text
[2, 4, 6, 8, 10]
```

All values are calculated and stored in a list.

## 17.2 What is Generator Expression?

### Definition

A Generator Expression is a concise way to create a generator object using parentheses.

### Example

```python
numbers = (i * 2 for i in range(1, 6))

print(numbers)
```

**Output:**

```text
<generator object <genexpr> at ...>
```

Values are generated when requested.

## 17.3 Differences

| List Comprehension | Generator Expression |
|---|---|
| Uses square brackets `[]`. | Uses parentheses `()`. |
| Creates a list. | Creates a generator object. |
| Uses eager evaluation. | Uses lazy evaluation. |
| Calculates all values immediately. | Calculates values when requested. |
| Stores all results in memory. | Produces results incrementally. |
| Supports indexing. | Does not support direct indexing. |
| Can be iterated multiple times. | Normally can be consumed only once. |
| Generally requires more memory for large results. | Generally requires less memory for large sequences. |

### Practical Example

```python
# List Comprehension

list_result = [i ** 2 for i in range(1, 6)]

# Generator Expression

gen_result = (i ** 2 for i in range(1, 6))

print(list_result)

print(next(gen_result))
print(next(gen_result))
```

**Output:**

```text
[1, 4, 9, 16, 25]
1
4
```

---

# 18. Real-Time Applications of Generators

Generators are useful in situations where processing data one element at a time is beneficial.

## 18.1 Reading Large Files

Instead of loading an entire file into memory using `readlines()`, we can process it line by line.

### Without a Generator

```python
def read_file():
    with open("data.txt", "r") as file:
        return file.readlines()


data = read_file()

for line in data:
    print(line)
```

Here, `readlines()` loads all lines into memory.

### With a Generator

```python
def read_file():
    with open("data.txt", "r") as file:
        for line in file:
            yield line


data = read_file()

for line in data:
    print(line)
```

Here, the generator produces one line at a time.

**Note:** The file remains open while the generator is being consumed. Make sure to consume or close the generator appropriately.

## 18.2 Processing Large Datasets

Generators are useful when processing large collections of data without creating intermediate lists.

Example:

```python
def process_numbers(numbers):
    for num in numbers:
        if num % 2 == 0:
            yield num


data = process_numbers(range(1, 11))

for value in data:
    print(value)
```

**Output:**

```text
2
4
6
8
10
```

## Other Applications

- Reading large CSV files.
- Processing logs.
- Data streaming.
- Generating sequences.
- Processing large datasets.
- Building data pipelines.

---

# 19. Important Interview Questions

### Q1. What is a Generator in Python?

A generator is a special type of iterator that produces values one at a time using the `yield` keyword.

### Q2. What is a Generator Function?

A generator function is a function that contains the `yield` keyword and produces values incrementally.

### Q3. What is the difference between `return` and `yield`?

`return` terminates the function, whereas `yield` produces a value and temporarily pauses execution.

### Q4. What is a Generator Object?

A generator object is an iterator created when a generator function is called.

### Q5. What is the purpose of `next()`?

`next()` retrieves the next available value from an iterator or generator.

### Q6. What is StopIteration?

StopIteration is an exception raised when an iterator or generator has no more values to produce.

### Q7. What is the difference between Iterable and Iterator?

An iterable can provide an iterator using `iter()`. An iterator produces values one at a time using `next()`.

### Q8. What is the difference between Iterator and Generator?

A generator is a special type of iterator created using `yield` or a generator expression. Other iterators can be created using `iter()` or custom iterator classes.

### Q9. Why do we use Generators?

Generators are useful for memory-efficient processing because they produce values incrementally instead of storing all results in memory.

### Q10. What is Lazy Evaluation?

Lazy evaluation means calculating values only when they are required. Generators use this technique to produce values on demand.

### Q11. What is the difference between `yield` and `yield from`?

`yield` produces a value, while `yield from` delegates value production to another iterable or generator.

### Q12. What are Generator Expressions?

Generator expressions are a compact way to create generator objects using parentheses instead of defining a generator function.

### Q13. Can we reuse an exhausted generator?

No. Once exhausted, a generator cannot be restarted. We need to call the generator function again to create a new generator object.

### Q14. What is the Iterator Protocol?

The iterator protocol defines two methods: `__iter__()` and `__next__()`. These methods allow an object to behave as an iterator.

### Q15. What is the difference between List Comprehension and Generator Expression?

List comprehension creates a list and calculates all values immediately. A generator expression creates a generator object and calculates values when requested.

---

# 20. Quick Revision

| Concept | Key Point |
|---|---|
| Generator | Produces values one at a time. |
| Generator Function | A function that contains `yield`. |
| `yield` | Produces a value and pauses execution. |
| `return` | Returns a value and terminates the function. |
| Generator Object | Object created when a generator function is called. |
| `next()` | Retrieves the next value. |
| StopIteration | Raised when no more values are available. |
| Iterable | An object that can provide an iterator. |
| Iterator | An object that produces values one at a time. |
| Generator Expression | Creates a generator using parentheses. |
| `yield from` | Delegates value production to another iterable or generator. |
| Lazy Evaluation | Calculates values only when requested. |
| Iterator Protocol | Uses `__iter__()` and `__next__()`. |
| Generator Exhaustion | Occurs when all generated values are consumed. |
| List Comprehension | Creates a list using square brackets. |

---

## Conclusion

Generators are an important Python concept used for producing and processing values incrementally.

The most important concepts to remember are:

1. `yield` pauses execution and produces a value.
2. Generator functions create generator objects.
3. `next()` retrieves values one at a time.
4. Generators follow the Iterator Protocol.
5. Generators use lazy evaluation.
6. Generators can improve memory efficiency when processing large sequences.
7. An exhausted generator cannot be restarted.

**Interview Preparation Tip:** Focus on understanding the execution flow of `yield`, `next()`, Lazy Evaluation, Iterator Protocol, and Generator Exhaustion. Practice writing generator functions independently rather than memorizing definitions.
