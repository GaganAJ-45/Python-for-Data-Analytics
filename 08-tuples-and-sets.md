# Tuples and Sets in Python

## PART 1 — TUPLES

---

## 1. What is a Tuple?

A tuple is a collection of items that is:
- **Ordered** — elements maintain insertion order
- **Immutable** — cannot be changed after creation
- **Allow duplicates** — same value can appear multiple times
- **Indexed** — accessed by position like a list

```python
my_tuple      = ("apple", "banana", "cherry")
numbers_tuple = (1, 2, 3, 4)
mixed_tuple   = ("AJ", 22, True, 3.14)
empty_tuple   = ()
nested_tuple  = ((1, 2), (3, 4))
```

**Where to use tuples:**
- Storing fixed data that should never change (RGB colors, coordinates, DB records)
- Returning multiple values from a function
- As dictionary keys (lists cannot be keys — tuples can)
- When you want to signal to other developers: "don't modify this"

---

## 2. Creating Tuples

```python
# With parentheses
t1 = (1, 2, 3)

# Without parentheses — tuple packing
t2 = 1, 2, 3
print(type(t2))   # Output: <class 'tuple'>

# Single element tuple — MUST have trailing comma
single = ("apple",)
print(type(single))         # Output: <class 'tuple'>

wrong  = ("apple")
print(type(wrong))          # Output: <class 'str'>  ← NOT a tuple!

# From a list
t3 = tuple([1, 2, 3])
print(t3)   # Output: (1, 2, 3)
```

> ⚠️ **Interview gotcha:** `("apple")` is just a string in parentheses, NOT a tuple. You must write `("apple",)` with the trailing comma.

---

## 3. Accessing Tuple Elements

Same as lists — indexing and slicing work identically.

```
Tuple:     a p p l e   b a n a n a   c h e r r y
Positive:  0           1             2
Negative: -3          -2            -1
```

```python
fruits = ("apple", "banana", "cherry")

print(fruits[0])    # Output: apple
print(fruits[-1])   # Output: cherry
print(fruits[1:3])  # Output: ('banana', 'cherry')
print(fruits[::-1]) # Output: ('cherry', 'banana', 'apple')
```

---

## 4. Tuples are Immutable

Once created, you **cannot** change, add, or remove elements.

```python
t = (1, 2, 3)
t[0] = 10    # ❌ TypeError: 'tuple' object does not support item assignment
t.append(4)  # ❌ AttributeError: 'tuple' object has no attribute 'append'
```

**Workaround — convert to list, modify, convert back:**
```python
t = (1, 2, 3)
lst = list(t)     # convert to list
lst[0] = 10       # modify
t = tuple(lst)    # convert back
print(t)          # Output: (10, 2, 3)
```

> **Why immutability matters:** It makes tuples **hashable** — they can be used as dictionary keys and stored in sets. Lists cannot because they are mutable.

---

## 5. Tuple Packing and Unpacking

### Packing — multiple values into one tuple
```python
# Python automatically packs multiple values into a tuple
point = 10, 20        # packing — no parentheses needed
print(point)          # Output: (10, 20)
print(type(point))    # Output: <class 'tuple'>

person = "AJ", 22, "Bengaluru"
print(person)         # Output: ('AJ', 22, 'Bengaluru')
```

### Unpacking — extract tuple values into variables
```python
point = (10, 20)
x, y = point          # unpacking
print(x)              # Output: 10
print(y)              # Output: 20

# Extended unpacking with *
first, *rest = (1, 2, 3, 4, 5)
print(first)          # Output: 1
print(rest)           # Output: [2, 3, 4, 5]

first, *middle, last = (1, 2, 3, 4, 5)
print(first, middle, last)   # Output: 1 [2, 3, 4] 5
```

### Swap variables using tuple unpacking
```python
a, b = 10, 20
a, b = b, a            # Python packs (b, a) as tuple, then unpacks
print(a, b)            # Output: 20 10
```

### Function returning multiple values
```python
def get_student():
    return "AJ", 22, "Bengaluru"   # returns a tuple

name, age, city = get_student()    # unpack directly
print(name, age, city)
```

> **Interview tip:** When a function returns multiple values in Python, it is technically returning a tuple. This is why you can unpack the return value directly.

---

## 6. Tuple Methods

Tuples have only **2 methods** — because they are immutable.

**`count(element)`** — number of occurrences
```python
t = (1, 2, 3, 1, 1)
print(t.count(1))   # Output: 3
```

**`index(element)`** — index of first occurrence, raises `ValueError` if not found
```python
t = ("apple", "banana", "cherry")
print(t.index("banana"))   # Output: 1

try:
    print(t.index("mango"))
except ValueError:
    print("Not found!")
```

---

## 7. Tuple Operations

```python
t1 = (1, 2, 3)
t2 = (4, 5, 6)

# Concatenation — creates new tuple
print(t1 + t2)    # Output: (1, 2, 3, 4, 5, 6)

# Repetition
print(t1 * 2)     # Output: (1, 2, 3, 1, 2, 3)

# Membership
print(2 in t1)    # Output: True

# Length
print(len(t1))    # Output: 3

# Min, Max, Sum
print(min(t1))    # Output: 1
print(max(t1))    # Output: 3
print(sum(t1))    # Output: 6
```

---

## 8. Named Tuples

`namedtuple` gives each position a name — makes code readable. From the `collections` module.

```python
from collections import namedtuple

# Define structure
Point   = namedtuple('Point', ['x', 'y'])
Student = namedtuple('Student', ['name', 'age', 'city'])

# Create instances
p = Point(10, 20)
s = Student("AJ", 22, "Bengaluru")

# Access by name (readable) or index
print(p.x, p.y)            # Output: 10 20
print(p[0], p[1])          # Output: 10 20  (still works like tuple)

print(s.name, s.age)       # Output: AJ 22
print(s)                   # Output: Student(name='AJ', age=22, city='Bengaluru')

# Still immutable
p.x = 100    # ❌ AttributeError — cannot modify
```

**Where to use:** Database rows, API responses, coordinates — anywhere you want the clarity of a class without the overhead.

---

## 9. Why Tuples Can Be Dictionary Keys — Lists Cannot

```python
# Tuple as dict key — works because tuples are hashable (immutable)
locations = {
    (28.6, 77.2): "Delhi",
    (12.9, 77.5): "Bengaluru",
    (19.0, 72.8): "Mumbai"
}
print(locations[(12.9, 77.5)])   # Output: Bengaluru

# List as dict key — fails because lists are not hashable (mutable)
d = {[1, 2]: "value"}   # ❌ TypeError: unhashable type: 'list'
```

> **Why hashable matters:** Dictionary keys and set elements must be **hashable** — meaning Python can compute a fixed hash value for them. Mutable objects like lists can change, so their hash would change too, breaking the dictionary. Immutable tuples always produce the same hash.

---

## PART 2 — SETS

---

## 10. What is a Set?

A set is a collection of items that is:
- **Unordered** — no guaranteed order of elements
- **Mutable** — you can add/remove elements
- **No duplicates** — automatically removes duplicate values
- **Unindexed** — cannot access by position

```python
fruits  = {"apple", "banana", "cherry"}
numbers = {1, 2, 3, 4, 5}

# Empty set — MUST use set(), not {}
empty_set  = set()      # ✅ correct
empty_dict = {}         # ❌ this creates an empty DICTIONARY, not set

print(type(empty_set))   # Output: <class 'set'>
print(type(empty_dict))  # Output: <class 'dict'>
```

**Where to use sets:**
- Removing duplicates from a list
- Fast membership testing — O(1) vs O(n) for lists
- Mathematical set operations (union, intersection, difference)
- Finding common or unique elements between collections

---

## 11. Creating Sets and Deduplication

```python
# From literal
s = {1, 2, 3, 2, 1}
print(s)   # Output: {1, 2, 3}  — duplicates removed automatically

# From list — most common use: remove duplicates
numbers = [1, 2, 2, 3, 3, 3, 4]
unique  = list(set(numbers))
print(unique)   # Output: [1, 2, 3, 4]

# From string — unique characters
chars = set("banana")
print(chars)   # Output: {'b', 'a', 'n'}

# From range
s = set(range(5))
print(s)   # Output: {0, 1, 2, 3, 4}
```

> **Interview tip:** `list(set(arr))` is the fastest one-liner to remove duplicates from a list. Time complexity O(n). But it does not preserve order — if order matters use `dict.fromkeys()` instead.

```python
# Remove duplicates AND preserve order (Python 3.7+)
nums = [3, 1, 2, 1, 3]
unique_ordered = list(dict.fromkeys(nums))
print(unique_ordered)   # Output: [3, 1, 2]
```

---

## 12. Set Methods

**`add(element)`** — adds one element. O(1).
```python
fruits = {"apple", "banana"}
fruits.add("cherry")
print(fruits)   # Output: {'apple', 'banana', 'cherry'}

fruits.add("apple")   # adding duplicate — no error, no change
print(fruits)         # Output: {'apple', 'banana', 'cherry'}
```

**`remove(element)`** — removes element, raises `KeyError` if not found.
```python
fruits.remove("banana")
print(fruits)   # Output: {'apple', 'cherry'}

fruits.remove("mango")   # ❌ KeyError: 'mango'
```

**`discard(element)`** — removes element, NO error if not found.
```python
fruits.discard("mango")   # ✅ no error — silent if not found
```

> **`remove()` vs `discard()`:**
> | | `remove()` | `discard()` |
> |---|---|---|
> | Element found | Removes it | Removes it |
> | Element NOT found | ❌ `KeyError` | ✅ No error |
> | Use when | Sure element exists | Not sure if exists |

**`pop()`** — removes and returns a **random** element (sets are unordered).
```python
s = {1, 2, 3, 4}
removed = s.pop()    # random element removed
print(removed)       # could be any element
```

**`clear()`** — removes all elements.
```python
fruits.clear()
print(fruits)   # Output: set()
```

**`copy()`** — shallow copy of the set.
```python
s1 = {1, 2, 3}
s2 = s1.copy()
s2.add(4)
print(s1)   # Output: {1, 2, 3}  — unchanged
```

---

## 13. Set Operations

Two ways to do each operation — **operator** or **method**.

```python
set1 = {1, 2, 3, 4}
set2 = {3, 4, 5, 6}
```

### Union — all elements from both sets
```python
print(set1 | set2)              # Output: {1, 2, 3, 4, 5, 6}
print(set1.union(set2))         # Output: {1, 2, 3, 4, 5, 6}
```

### Intersection — elements common to both
```python
print(set1 & set2)              # Output: {3, 4}
print(set1.intersection(set2))  # Output: {3, 4}
```

### Difference — in set1 but NOT in set2
```python
print(set1 - set2)              # Output: {1, 2}
print(set1.difference(set2))    # Output: {1, 2}

print(set2 - set1)              # Output: {5, 6}  ← order matters!
```

### Symmetric Difference — in either but NOT in both
```python
print(set1 ^ set2)                       # Output: {1, 2, 5, 6}
print(set1.symmetric_difference(set2))   # Output: {1, 2, 5, 6}
```

---

## 14. Set Relationship Methods

**`issubset()`** — is every element of this set in the other set?
```python
a = {1, 2}
b = {1, 2, 3, 4}
print(a.issubset(b))    # Output: True  — all of a is in b
print(b.issubset(a))    # Output: False
print(a <= b)           # Output: True  — same as issubset
```

**`issuperset()`** — does this set contain all elements of the other?
```python
print(b.issuperset(a))   # Output: True  — b contains all of a
print(b >= a)            # Output: True  — same as issuperset
```

**`isdisjoint()`** — do the sets share NO common elements?
```python
x = {1, 2, 3}
y = {4, 5, 6}
z = {3, 4, 5}

print(x.isdisjoint(y))   # Output: True  — no common elements
print(x.isdisjoint(z))   # Output: False — 3 is common
```

---

## 15. `frozenset` — Immutable Set

A `frozenset` is a set that **cannot be modified** after creation. It is hashable — so it can be used as a dictionary key or stored inside another set.

```python
fs = frozenset([1, 2, 3, 2, 1])
print(fs)              # Output: frozenset({1, 2, 3})

fs.add(4)              # ❌ AttributeError — frozenset is immutable

# Can be used as dict key
d = {frozenset({1, 2}): "pair"}
print(d)

# Can be stored inside a set
s = {frozenset({1, 2}), frozenset({3, 4})}
```

> **frozenset vs set** → same as tuple vs list. Use frozenset when you need set operations but the set itself must not change.

---

## 16. Time Complexity — Must Know for Interviews

### Tuple
| Operation | Time |
|---|---|
| Access by index | O(1) |
| Search (`in`) | O(n) |
| `count()` | O(n) |
| `index()` | O(n) |
| Length `len()` | O(1) |

### Set
| Operation | Time |
|---|---|
| Add `add()` | O(1) avg |
| Remove `remove()` / `discard()` | O(1) avg |
| Search `in` | **O(1) avg** |
| Union `\|` | O(len(s1) + len(s2)) |
| Intersection `&` | O(min(len(s1), len(s2))) |

> **Most important:** Set `in` operator is **O(1)** — this is why sets are used for fast lookup in DSA. List `in` is O(n). This single difference drives many interview optimization questions.

---

## 17. List vs Tuple vs Set — Full Comparison

| Feature | List | Tuple | Set |
|---|---|---|---|
| Ordered | ✅ | ✅ | ❌ |
| Mutable | ✅ | ❌ | ✅ |
| Duplicates | ✅ | ✅ | ❌ |
| Indexed | ✅ | ✅ | ❌ |
| Hashable | ❌ | ✅ | ❌ |
| `in` operator | O(n) | O(n) | O(1) |
| Dict key? | ❌ | ✅ | ❌ |
| Use for | General collection | Fixed data | Unique + fast lookup |

---

## Quick Reference

```python
# TUPLE
t = (1, 2, 3)         # create
t = 1, 2, 3           # packing
t = (1,)              # single element — comma required
a, b, c = t           # unpacking
first, *rest = t      # extended unpacking
t.count(x)            # count occurrences
t.index(x)            # find index
t + (4, 5)            # concatenation
x in t                # membership — O(n)

# NAMEDTUPLE
from collections import namedtuple
Point = namedtuple('Point', ['x', 'y'])
p = Point(10, 20)
p.x                   # access by name

# SET
s = {1, 2, 3}         # create
s = set()             # empty set (NOT {})
s.add(x)              # add element
s.remove(x)           # remove — KeyError if missing
s.discard(x)          # remove — no error if missing
s.pop()               # remove random element
s.clear()             # empty the set
x in s                # membership — O(1)

# SET OPERATIONS
s1 | s2               # union
s1 & s2               # intersection
s1 - s2               # difference
s1 ^ s2               # symmetric difference
s1.issubset(s2)       # s1 ⊆ s2
s1.issuperset(s2)     # s1 ⊇ s2
s1.isdisjoint(s2)     # no common elements

# DEDUPLICATE
unique = list(set(arr))             # fast — doesn't preserve order
unique = list(dict.fromkeys(arr))   # preserves order

# FROZENSET
fs = frozenset([1, 2, 3])          # immutable set
```

---

## Interview Short Answers

**Q: What is the difference between a list and a tuple?**
> Both are ordered and allow duplicates, but lists are mutable — you can add, remove, or change elements. Tuples are immutable — once created they cannot be changed. Tuples are faster than lists, hashable, and can be used as dictionary keys. Use tuples for fixed data, lists for dynamic data.

**Q: How do you create a tuple with one element?**
> You must include a trailing comma: `t = ("apple",)`. Without the comma, `("apple")` is just a string in parentheses — Python does not treat it as a tuple. This is a very common beginner mistake.

**Q: Why can tuples be used as dictionary keys but not lists?**
> Dictionary keys must be hashable — Python computes a fixed hash value for them. Tuples are immutable so their hash never changes, making them hashable. Lists are mutable — their content can change, so their hash would change too, which would break the dictionary. That is why lists cannot be used as dictionary keys.

**Q: What is the difference between `remove()` and `discard()` in a set?**
> Both remove an element from a set. The difference is in error handling — `remove()` raises a `KeyError` if the element is not found, while `discard()` silently does nothing. Use `discard()` when you are not sure if the element exists.

**Q: Why is `in` O(1) for sets but O(n) for lists?**
> Sets use a hash table internally. When you check `x in set`, Python computes the hash of `x` and directly looks up that position in the hash table — constant time regardless of set size. Lists store elements sequentially, so Python must check each element one by one — linear time. This is why sets are preferred for fast membership testing in DSA.

**Q: What is the difference between a set and a frozenset?**
> A set is mutable — you can add and remove elements. A frozenset is immutable — it cannot be changed after creation. Because frozensets are immutable, they are hashable and can be used as dictionary keys or stored inside other sets. The relationship is the same as list vs tuple.

**Q: How do you remove duplicates from a list in Python?**
> The fastest way is `list(set(arr))` — converting to a set removes duplicates in O(n), then converting back to a list. However, this does not preserve the original order. If order matters, use `list(dict.fromkeys(arr))` which preserves insertion order in Python 3.7+.

**Q: What is tuple packing and unpacking?**
> Packing is assigning multiple values to a single tuple variable: `t = 1, 2, 3`. Python automatically wraps them in a tuple. Unpacking is extracting tuple elements into separate variables: `a, b, c = t`. This is used in function returns, swapping variables (`a, b = b, a`), and `for` loops with `enumerate()` and `zip()`.
