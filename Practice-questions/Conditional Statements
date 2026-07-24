# Python Practice: Conditional Statements (if / elif / else)

Daily practice problems using `if`, `elif`, `else`, and nested conditionals.

Click a question to jump straight to its solution and sample output. Try solving it yourself first! If you spot a bug, have a better approach, or have a doubt about any solution — open an issue or drop a comment.

## Questions

1. [Check whether a given number is even or odd.](#1-even-or-odd)
2. [Check whether a given number is positive or negative.](#2-positive-or-negative)
3. [Given two numbers `a` and `b`, find which one is greater.](#3-greater-of-two-numbers)
4. [Check whether a given year is a leap year.](#4-leap-year-check)
5. [Check whether a person is eligible to vote based on age (18+).](#5-voting-eligibility)
6. [Check whether a given number is divisible by 3.](#6-divisible-by-3)
7. [Check whether a given character is a vowel or a consonant.](#7-vowel-or-consonant)
8. [Check whether a given number lies between 1 and 100.](#8-number-between-1-and-100)
9. [Check whether a number is positive, negative, or zero.](#9-positive-negative-or-zero)
10. [Given total marks and obtained marks, calculate the percentage and print the student's grade.](#10-student-grade-calculator)
11. [Check whether a given number is a 1-digit, 2-digit, or 3-digit number.](#11-count-digits-1-2-or-3-digit)
12. [Check whether a given number is divisible by 5, by 3, by both, or neither.](#12-divisible-by-5-3-or-both)
13. [Check whether a given character is uppercase, lowercase, or neither.](#13-uppercase-or-lowercase-check)
14. [Validate whether a given day/month/year forms a valid calendar date.](#14-validate-a-date)
15. [Build a simple calculator using `+ - * ** / // %`.](#15-simple-calculator)
16. [Given the cost of 5 items, apply a nested discount: 15% off if the total exceeds ₹500.](#16-nested-discount-on-total-purchase)
17. [Build a simple login system that checks username and password.](#17-simple-login-system)
18. [Build a simple banking system that validates account, PIN, and withdrawal.](#18-simple-banking-system)
19. [Given three numbers, find the largest among them.](#19-largest-of-three-numbers)

---

## Solutions

### 1. Even or Odd
```python
num = int(input("Enter the Number: "))
if (num % 2 == 0):
    print(f"The Number {num} is Even")
else:
    print("It is odd")
```
**Sample input:** `7`
**Output:**
```
It is odd
```

### 2. Positive or Negative
```python
num1 = int(input("Enter The Number: "))
if (num1 < 0):
    print(f"entered number is negative: {num1}")
else:
    print(f"positive number {num1}")
```
**Sample input:** `-5`
**Output:**
```
entered number is negative: -5
```

### 3. Greater of Two Numbers
```python
a = int(input("enter a value: "))
b = int(input("enter b value: "))
if (a > b):
    print("a is the greater value")
elif (b > a):
    print("b is the greater value")
else:
    print("enter the correct value")
```
**Sample input:** `10`, `4`
**Output:**
```
a is the greater value
```

### 4. Leap Year Check
```python
c = int(input("Enter the year: "))
if (c % 400 == 0 or (c % 4 == 0 and c % 100 != 0)):
    print(f"it is a leap year {c}")
else:
    print("it is not a leap year")
```
**Sample input:** `2024`
**Output:**
```
it is a leap year 2024
```

### 5. Voting Eligibility
```python
age = int(input("Enter the age: "))
if (age >= 18):
    print("The person is eligible to vote")
else:
    print("the person is not eligible")
```
**Sample input:** `20`
**Output:**
```
The person is eligible to vote
```

### 6. Divisible by 3
```python
d = int(input("enter the number: "))
if (d % 3 == 0):
    print("the number can be divided by 3")
else:
    print("the number is not divisible by 3")
```
**Sample input:** `9`
**Output:**
```
the number can be divided by 3
```

### 7. Vowel or Consonant
```python
char = input("Enter the character: ").lower()
vowels = ["a", "e", "i", "o", "u"]
if (char in vowels):
    print("it is a Vowel")
else:
    print("it is a Consonant")
```
**Sample input:** `e`
**Output:**
```
it is a Vowel
```

### 8. Number Between 1 and 100
```python
f = int(input("Enter the number: "))
if (f > 0 and f < 100):
    print("the number is between 1 to 100")
else:
    print("the number is not between 1 to 100")
```
**Sample input:** `50`
**Output:**
```
the number is between 1 to 100
```

### 9. Positive Negative or Zero
```python
a = int(input("Enter the Number: "))
if (a > 0):
    print("It Is +Ve")
elif (a < 0):
    print("It Is -Ve")
else:
    print("It Is 0")
```
**Sample input:** `0`
**Output:**
```
It Is 0
```

### 10. Student Grade Calculator
```python
marks = int(input("Enter the total marks: "))
obt_marks = int(input("Enter the obtained marks: "))
percentage_of_stu = (obt_marks / marks) * 100
print(f"The percentage of the student is {percentage_of_stu}%")

if (percentage_of_stu > 90):
    print("The student obtained Distinction")
elif (80 <= percentage_of_stu <= 89):
    print("The student obtained 1st class")
elif (70 <= percentage_of_stu <= 79):
    print("The student obtained 2nd class")
else:
    print("The Student just passed")
```
> Note: fixed the original range checks (`80 < ... < 89` skipped exactly 80 and 89) to use `<=` so boundary values are included.

**Sample input:** `500`, `460`
**Output:**
```
The percentage of the student is 92.0%
The student obtained Distinction
```

### 11. Count Digits (1, 2, or 3 digit)
```python
num = int(input("Enter the number: "))

if (0 < num <= 9):
    print("The Number is 1 digit")
elif (9 < num < 100):
    print("The Number is 2 digit")
elif (99 < num < 1000):
    print("The Number is 3 digit")
else:
    print("Entered Number is more than 3 digits or negative")
```
**Sample input:** `45`
**Output:**
```
The Number is 2 digit
```

### 12. Divisible by 5, 3, or Both
```python
num = int(input("Enter the Number: "))
a = (num % 5) == 0
b = (num % 3) == 0

if (a and b):
    print("The given number is divisible by both 5 and 3")
elif (a is True):
    print("the given number is divisible by 5")
elif (b is True):
    print("the given number is divisible by 3")
else:
    print("the given number is not divisible by 5 or 3")
```
> Note: added the missing `else` branch — the original had no output for numbers divisible by neither.

**Sample input:** `15`
**Output:**
```
The given number is divisible by both 5 and 3
```

### 13. Uppercase or Lowercase Check
```python
char = input("Enter the char: ")
if (char >= "A" and char <= "Z"):
    print("upper")
elif (char >= "a" and char <= "z"):
    print("lower")
else:
    print("other")
```
> Note: changed `< "Z"` and `< "z"` to `<=` so "Z" and "z" themselves are classified correctly.

**Sample input:** `G`
**Output:**
```
upper
```

### 14. Validate a Date
```python
day = int(input("Enter The Day: "))
month = int(input("Enter The Month: "))
year = int(input("Enter The Year: "))

if (year % 400 == 0) or (year % 4 == 0 and year % 100 != 0):
    leap = True
else:
    leap = False

if (month < 1 or month > 12):
    print("Invalid month, enter the month correctly")
elif (day < 1):
    print("Invalid date, enter the day correctly")
elif (month in [1, 3, 5, 7, 8, 10, 12]):
    print("valid Date" if day <= 31 else "invalid date")
elif (month in [4, 6, 9, 11]):
    print("valid Date" if day <= 30 else "invalid date")
elif (month == 2):
    if leap:
        print("valid Date" if day <= 29 else "Invalid Date")
    else:
        print("valid date" if day <= 28 else "invalid date")
```
> Note: fixed the non-leap-February check — original said `day < 29` (which wrongly allowed day 0) and should be `day <= 28`.

**Sample input:** `29`, `2`, `2024`
**Output:**
```
valid Date
```

### 15. Simple Calculator
```python
a = int(input("Enter a 1st number: "))
b = int(input("Enter a 2nd number: "))
c = input("Enter the operator: ")

if (c == "+"):
    ans = a + b
    print(f"{a} + {b} = {ans}")
elif (c == "-"):
    ans = a - b
    print(f"{a} - {b} = {ans}")
elif (c == "*"):
    ans = a * b
    print(f"{a} * {b} = {ans}")
elif (c == "**"):
    ans = a ** b
    print(f"{a} ** {b} = {ans}")
elif (c == "/"):
    ans = a / b
    print(f"{a} / {b} = {ans}")
elif (c == "//"):
    ans = a // b
    print(f"{a} // {b} = {ans}")
elif (c == "%"):
    ans = a % b
    print(f"{a} % {b} = {ans}")
else:
    print("Enter a valid Operator")
```
**Sample input:** `10`, `5`, `+`
**Output:**
```
10 + 5 = 15
```

### 16. Nested Discount on Total Purchase
```python
apple = int(input("Enter the Item: "))
banana = int(input("Enter the Item: "))
mango = int(input("Enter the Item: "))
orange = int(input("Enter the Item: "))
watermelon = int(input("Enter the amt: "))

total = apple + banana + mango + orange + watermelon

if (total > 400):
    if (total > 500):
        discount = (15 / 100) * total
        print(f"15% discount applied, the total amt is {total - discount}")
    else:
        print(f"No extra discount, total amt is {total}")
else:
    print(f"No discount, total amt is {total}")
```
> Note: added the missing `else` branches — the original only printed something when `total > 500`; totals between 401–500 and totals ≤ 400 produced no output. Also fixed the printed amount to show the *discounted* total, not just the discount value.

**Sample input:** `100`, `150`, `200`, `100`, `50`
**Output:**
```
15% discount applied, the total amt is 510.0
```

### 17. Simple Login System
```python
username = input("Enter The User Name: ")
Password = int(input("Enter The Password: "))
name = "Gagan_a_j"
password_user = 4522

if (username == name):
    if (password_user == Password):
        print("Login Successful")
    else:
        print("Incorrect Password")
else:
    print("Enter the correct User name")
```
**Sample input:** `Gagan_a_j`, `4522`
**Output:**
```
Login Successful
```

### 18. Simple Banking System
```python
acc_num = int(input("Enter The acc num: "))
pin = int(input("Enter The Password: "))
amt_withdraw = int(input("Enter The Amt To withDraw: "))
account_num = 123456789
password = 4522
total_amt = 50000

if (acc_num == account_num):
    if (pin == password):
        if (amt_withdraw > total_amt):
            print("Withdraw amt is Greater than the balance")
        else:
            total_amt = total_amt - amt_withdraw
            print(f"Successfully amount is withdrawn")
            print(f"Balance is {total_amt}")
    else:
        print("Enter the correct pin")
else:
    print("Enter the correct account number")
```
**Sample input:** `123456789`, `4522`, `1000`
**Output:**
```
Successfully amount is withdrawn
Balance is 49000
```

### 19. Largest of Three Numbers
```python
a = int(input("Enter the a value: "))
b = int(input("Enter the b value: "))
c = int(input("Enter the c value: "))

if (a > b and a > c):
    print("A is greater")
elif (b > a and b > c):
    print("B is greater")
else:
    print("C is greater")
```
> Note: rewrote the comparison logic — the original chained comparisons (`c < a > b`) produced wrong results for some inputs (e.g., ties, or cases where `c` was actually the largest). This version compares each variable directly against the other two.

**Sample input:** `3`, `9`, `5`
**Output:**
```
B is greater
```
