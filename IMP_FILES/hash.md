# Python: Functions, Methods, Iterable & Hashable

## 1. Function

A **function** is a reusable block of code that performs a specific task.

A function is called directly using its name.

Example:

    def add(a, b):
        return a + b

    print(add(10, 20))

Output:

    30

### Built-in Functions

Built-in functions are functions already provided by Python.

Examples:

- `print()`
- `input()`
- `len()`
- `type()`
- `sum()`
- `max()`
- `min()`
- `abs()`
- `sorted()`
- `range()`

Example:

    numbers = [10, 20, 30]

    print(len(numbers))
    print(sum(numbers))

Here:

- `len()` → Built-in function
- `sum()` → Built-in function

Functions are called directly:

    len(numbers)
    sum(numbers)


---

# 2. Method

A **method** is a function that belongs to an object or class.

A method is normally called using the dot `.` operator.

Example:

    text = "python"

    print(text.upper())

Here:

- `text` → Object
- `upper()` → Method

Another example:

    numbers = [10, 20, 30]

    numbers.append(40)

Here:

- `numbers` → List object
- `append()` → List method

### Function vs Method

    len(numbers)          # Function
    numbers.append(40)    # Method

Simple rule:

    Function → function(object)

    Method → object.method()


---

# 3. Iterable

An **iterable** is an object whose elements can be accessed one by one.

Usually, we can use an iterable with a `for` loop.

Example:

    numbers = [10, 20, 30]

    for x in numbers:
        print(x)

Output:

    10
    20
    30

Since we can access the elements one by one, a list is an iterable.

### Common Iterable Objects

- List
- Tuple
- Set
- Dictionary
- String
- Range

Example:

    for x in [10, 20, 30]:
        print(x)

    for x in (10, 20, 30):
        print(x)

    for x in {10, 20, 30}:
        print(x)

    for x in "Python":
        print(x)

    for x in range(5):
        print(x)

### Simple Definition

> **Iterable = An object whose elements can be accessed one by one.**


---

# 4. Hash Value

A **hash value** is an integer generated from an object using Python's `hash()` function.

Example:

    print(hash(10))
    print(hash("Python"))

The result is an integer.

Conceptually:

    Object
       ↓
     hash()
       ↓
    Integer
       ↓
    Used for lookup

Example:

    x = "Python"

    print(hash(x))
    print(hash(x))

During the same Python execution, a hashable object's hash value remains consistent.

However, for some types such as strings, the hash value can be different when Python is started again.

So:

> **Hash values do not necessarily stay the same across different Python executions.**

But during the relevant execution, a hashable object's hash must remain consistent.


---

# 5. Why is Hashing Important?

Hashing is mainly used by:

- Sets
- Dictionaries

Hashing allows Python to find items quickly.

Think of a hash value like a **location number**.

    Object
       ↓
     hash()
       ↓
    Hash Value
       ↓
    Find location
       ↓
      Data

Instead of checking every item one by one, a hash-based data structure can use the hash to quickly find where an item should be.

This is why:

- Set membership is generally very fast.
- Dictionary key lookup is generally very fast.


---

# 6. Real Example: Dictionary

Consider:

    student = {
        "name": "Gagan",
        "age": 22
    }

When we write:

    student["age"]

Conceptually, Python can use the hash of `"age"` to find the key:

    "age"
      ↓
    hash("age")
      ↓
    Hash Value
      ↓
    Find location
      ↓
    "age" → 22

This is a simplified explanation of dictionary lookup.

The actual Python implementation is more complex.


---

# 7. Hashable

An object is **hashable** if it can safely provide a stable hash value and can therefore be used in a hash-based collection.

Hashable objects can be:

1. Used as dictionary keys.
2. Used as elements of a set.

Examples of hashable objects:

- Integers
- Strings
- Floats
- Booleans
- Suitable tuples

Example:

    hash(10)

    hash("Python")

    hash((10, 20))

These work because these objects are hashable.


---

# 8. Why is a List Not Hashable?

A list is **mutable**.

Mutable means that its contents can be changed.

Example:

    numbers = [10, 20, 30]

    numbers.append(40)

    print(numbers)

Output:

    [10, 20, 30, 40]

Because a list can change, Python does not allow a list to be hashable.

Example:

    hash([10, 20, 30])

Error:

    TypeError: unhashable type: 'list'

A list also cannot be used as a dictionary key.

Example:

    student = {
        [10, 20]: "Gagan"
    }

This gives an error because the list is not hashable.


---

# 9. Why Does Mutability Matter?

Imagine a list:

    numbers = [10, 20, 30]

Suppose Python allowed the list to be a dictionary key.

Conceptually:

    [10, 20, 30]
          ↓
        hash
          ↓
      Location 50

Now the list changes:

    numbers.append(40)

The list becomes:

    [10, 20, 30, 40]

If its hash changed, the location could also change:

    Before:

    [10, 20, 30]
          ↓
        hash
          ↓
      Location 50


    After:

    [10, 20, 30, 40]
          ↓
     different hash
          ↓
      Location 80

But the dictionary originally stored information using the old location.

This would make lookup unreliable.

Therefore:

> **Mutable objects such as lists are not hashable.**


---

# 10. Tuple and Hashing

A tuple is **immutable**.

Example:

    point = (10, 20)

We cannot change its elements.

    point[0] = 50

This gives an error.

Because a tuple is immutable, it can be hashable.

Example:

    hash((10, 20))

This works.

Therefore, a tuple can be used as a dictionary key:

    locations = {
        (10, 20): "Home"
    }

### Important Rule

A tuple is hashable **only if all of its elements are hashable**.

This works:

    hash((10, 20))

because integers are hashable.

This does not work:

    hash(([10, 20], 30))

because the tuple contains a list, and a list is not hashable.


---

# 11. List

A **list** is an ordered, mutable, iterable collection that allows duplicate elements.

Example:

    numbers = [10, 20, 20, 30]

### Properties

- Ordered → Yes
- Mutable → Yes
- Duplicates → Yes
- Iterable → Yes
- Hashable → No
- Indexing → Yes

Example:

    numbers = [10, 20, 30]

    print(numbers[0])

Output:

    10

We can modify a list:

    numbers[0] = 100
    numbers.append(40)


---

# 12. Tuple

A **tuple** is an ordered, immutable, iterable collection that allows duplicate elements.

Example:

    numbers = (10, 20, 20, 30)

### Properties

- Ordered → Yes
- Mutable → No
- Duplicates → Yes
- Iterable → Yes
- Hashable → Yes, if all elements are hashable
- Indexing → Yes

Example:

    numbers = (10, 20, 30)

    print(numbers[0])

Output:

    10

We cannot modify a tuple:

    numbers[0] = 100

This gives an error because tuples are immutable.


---

# 13. Set

A **set** is an unordered, mutable, iterable collection that stores unique hashable elements.

Example:

    numbers = {10, 20, 30}

Sets do not allow duplicate elements.

Example:

    numbers = {10, 20, 20, 30}

The duplicate `20` is stored only once.

### Properties

- Ordered → No
- Mutable → Yes
- Duplicates → No
- Iterable → Yes
- Elements must be hashable → Yes
- Indexing → No

Example:

    numbers = {10, 20, 30}

    numbers.add(40)

The set itself is mutable.

But its elements must be hashable.

This works:

    numbers = {10, 20, (30, 40)}

This does not:

    numbers = {10, 20, [30, 40]}

because a list is not hashable.


---

# 14. Dictionary

A **dictionary** is a mutable collection of key-value pairs.

Example:

    student = {
        "name": "Gagan",
        "age": 22,
        "branch": "ECE"
    }

It contains:

    Key       Value
    ----------------
    "name"    "Gagan"
    "age"     22
    "branch"  "ECE"

### Properties

- Ordered → Yes, insertion order
- Mutable → Yes
- Duplicate keys → No
- Iterable → Yes
- Keys must be hashable → Yes
- Values must be hashable → No
- Indexing → No


---

# 15. Dictionary Keys and Values

## Keys

Dictionary keys must be hashable.

This works:

    student = {
        "name": "Gagan",
        10: "Ten",
        (1, 2): "Tuple"
    }

This does not work:

    student = {
        [1, 2]: "List"
    }

because a list is not hashable.

## Values

Dictionary values do not need to be hashable.

This is valid:

    student = {
        "name": "Gagan",
        "marks": [80, 90, 85]
    }

The value is a list, and that is allowed.

Therefore:

    Dictionary

    Key   → Must be hashable
    Value → Can be any type


---

# 16. Dictionary Iteration

A dictionary is iterable.

When we directly iterate over a dictionary, we get its keys.

Example:

    student = {
        "name": "Gagan",
        "age": 22
    }

    for key in student:
        print(key)

Output:

    name
    age

To get values:

    for value in student.values():
        print(value)

To get both keys and values:

    for key, value in student.items():
        print(key, value)


---

# 17. Set: remove() vs discard()

Example:

    numbers = {10, 20, 30}

    numbers.remove(20)

`20` exists, so it is removed.

If the element does not exist:

    numbers.remove(50)

Python raises:

    KeyError: 50

Why?

Because `remove()` expects the element to exist.

### discard()

    numbers.discard(50)

If `50` does not exist, `discard()` does nothing.

So:

    remove()  → Error if element does not exist
    discard() → No error if element does not exist


---

# 18. List vs Tuple vs Set vs Dictionary

| Feature | List | Tuple | Set | Dictionary |
|---|---|---|---|---|
| Ordered | Yes | Yes | No | Yes |
| Mutable | Yes | No | Yes | Yes |
| Duplicates | Yes | Yes | No | Keys: No |
| Iterable | Yes | Yes | Yes | Yes |
| Hashable | No | Sometimes | No | No |
| Uses hashing | No | No | Yes | Yes |
| Indexing | Yes | Yes | No | No |
| Main purpose | Collection of items | Fixed collection | Unique items | Key-value mapping |


---

# 19. Important Hashability Rules

    Integer      → Hashable
    String       → Hashable
    Float        → Hashable
    Boolean      → Hashable

    Tuple        → Hashable if all elements are hashable

    List         → Not hashable
    Set          → Not hashable
    Dictionary   → Not hashable

For a set:

    Set elements → Must be hashable

For a dictionary:

    Keys         → Must be hashable
    Values       → Do not need to be hashable


---

# 20. Iterable vs Hashable

These are two different concepts.

## Iterable

Means:

> "Can I access the elements one by one?"

Example:

    numbers = [10, 20, 30]

    for x in numbers:
        print(x)

The list is iterable.

## Hashable

Means:

> "Can Python safely calculate and use a hash value for this object in a hash-based collection?"

Example:

    hash(10)

The integer is hashable.


---

# 21. Important Examples

## List

    x = [1, 2, 3]

    # Iterable
    for i in x:
        print(i)

    # Not hashable
    hash(x)          # TypeError


## Tuple

    x = (1, 2, 3)

    # Iterable
    for i in x:
        print(i)

    # Hashable
    hash(x)          # Works


## Set

    x = {1, 2, 3}

    # Iterable
    for i in x:
        print(i)

    # Set itself is not hashable
    hash(x)          # TypeError


## Dictionary

    student = {
        "name": "Gagan",
        "age": 22
    }

    # Iterable
    for key in student:
        print(key)


---

# 22. Final Mental Model

## List

    Ordered
    Mutable
    Duplicates allowed
    Iterable
    Not hashable

## Tuple

    Ordered
    Immutable
    Duplicates allowed
    Iterable
    Hashable if all elements are hashable

## Set

    Unordered
    Mutable
    Unique elements
    Iterable
    Elements must be hashable

## Dictionary

    Key → Value
    Mutable
    Iterable
    Keys must be hashable
    Values can be any type


---

# 23. Most Important Points

1. **Function** → Reusable block of code called directly.

2. **Method** → Function associated with an object or class.

3. **Iterable** → Object whose elements can be accessed one by one.

4. **Hash value** → Integer generated from an object for hash-based lookup.

5. **Hashable** → Object that can safely be used in a set or as a dictionary key.

6. **List** → Mutable, iterable, and not hashable.

7. **Tuple** → Immutable, iterable, and hashable when all its elements are hashable.

8. **Set** → Stores unique hashable elements.

9. **Dictionary** → Stores key-value pairs; keys must be hashable.

10. **Dictionary values do not need to be hashable.**

11. `remove()` raises `KeyError` when a set element is not found.

12. `discard()` does not raise an error when a set element is not found.

13. Hash values can differ between separate Python executions for some types, but remain consistent for a hashable object during the relevant execution.

### Easy Memory Trick

    Iterable
    → "Can I go through it?"

    Hashable
    → "Can I safely use it in a set or as a dictionary key?"

    Mutable
    → "Can I change it?"

    Immutable
    → "Can I NOT change it?"
