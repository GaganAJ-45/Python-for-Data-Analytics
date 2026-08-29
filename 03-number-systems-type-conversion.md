## **Number Systems and Type Conversion in Python**

### **1. The `int` Type**

- `int` represents **only integer numbers, without a decimal point**.
- You can check the type of a number using:
```python
num = 89
print(type(num))
```
- To check the class of an integer:
```python
print(num.__class__)   # <class 'int'>
```

---

### **2. Converting Decimal (int) to Binary, Octal, or Hexadecimal**

An integer (base 10 / decimal) can be converted into:

```
int (decimal)
  ├── Binary  → Base 2
  ├── Octal   → Base 8
  └── Hex     → Base 16
```

Python has built-in functions for each of these conversions:

```python
num = 89
print(bin(num))   # Binary
print(oct(num))   # Octal
print(hex(num))   # Hexadecimal
```

---

### **3. Manual Conversion — Decimal to Binary**

To convert a decimal number to binary, repeatedly divide by 2 and record the remainders. Read the remainders from **bottom to top**.

**Example: Convert 89 to binary**

| Step | Division | Quotient | Remainder |
|------|----------|----------|-----------|
| 1 | 89 / 2 | 44 | 1 |
| 2 | 44 / 2 | 22 | 0 |
| 3 | 22 / 2 | 11 | 0 |
| 4 | 11 / 2 | 5  | 1 |
| 5 | 5 / 2  | 2  | 1 |
| 6 | 2 / 2  | 1  | 0 |
| 7 | 1 / 2  | 0  | 1 |

Reading the remainders bottom to top:

**89 → 1011001₂**

---

### **4. Manual Conversion — Decimal to Octal**

Repeatedly divide by 8 and record the remainders (bottom to top).

**Example: Convert 89 to octal**

| Step | Division | Quotient | Remainder |
|------|----------|----------|-----------|
| 1 | 89 / 8 | 11 | 1 |
| 2 | 11 / 8 | 1  | 3 |
| 3 | 1 / 8  | 0  | 1 |

**89 → 131₈**

---

### **5. Manual Conversion — Decimal to Hexadecimal**

Repeatedly divide by 16. If a remainder is greater than 9, convert it to the corresponding hex letter (10=A, 11=B, 12=C, 13=D, 14=E, 15=F).

**Example: Convert 89 to hex**

| Step | Division | Quotient | Remainder |
|------|----------|----------|-----------|
| 1 | 89 / 16 | 5 | 9 |
| 2 | 5 / 16  | 0 | 5 |

**89 → 59₁₆**

---

### **6. Manual Conversion — Binary to Decimal**

Multiply each binary digit by 2 raised to its positional power (starting from 0 on the right), then sum the results.

**Example: Convert 1011010₂ to decimal**

```
(1 × 2⁶) = 64
(0 × 2⁵) = 0
(1 × 2⁴) = 16
(1 × 2³) = 8
(0 × 2²) = 0
(1 × 2¹) = 2
(0 × 2⁰) = 0
-----------------
Sum       = 90
```

**1011010₂ → 90**

---

### **7. Manual Conversion — Octal to Decimal**

Multiply each octal digit by 8 raised to its positional power, then sum.

**Example: Convert 132₈ to decimal**

```
(1 × 8²) = 64
(3 × 8¹) = 24
(2 × 8⁰) = 2
-----------------
Sum       = 90
```

**132₈ → 90**

---

### **8. Quick Reference — Python Built-in Conversion Functions**

| Conversion | Function | Example | Output |
|---|---|---|---|
| int → Binary | `bin()` | `bin(90)` | `'0b1011010'` |
| int → Octal | `oct()` | `oct(90)` | `'0o132'` |
| int → Hex | `hex()` | `hex(90)` | `'0x5a'` |
| Binary string → int | `int(x, 2)` | `int('1011010', 2)` | `90` |
| Octal string → int | `int(x, 8)` | `int('132', 8)` | `90` |
| Hex string → int | `int(x, 16)` | `int('5a', 16)` | `90` |
