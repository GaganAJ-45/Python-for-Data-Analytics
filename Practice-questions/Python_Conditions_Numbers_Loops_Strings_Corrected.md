# Practice Questions — Python Conditions, Numbers, Loops & Strings

> From Easy to Hard | Beginner → DSA Interview Ready  
> All solutions below are corrected and checked for the logic issues from the original practice set.

---

## How to Use This File

- Try solving each question yourself first.
- Read the **Hint** only if you are stuck.
- Read the **Tip** to understand the pattern and common mistakes.
- For number/digit problems, prefer **numeric manipulation** with `% 10` and `// 10` instead of converting the number to a string.
- Study the pattern behind each solution, not just the final code.

---

# 🟢 EASY — CONDITIONS & BASIC LOOPS

---

## Q1. Check Even or Odd

```python
num = int(input("Enter the number: "))

if num % 2 == 0:
    print(f"{num} is Even")
else:
    print(f"{num} is Odd")
```

**Pattern:** `num % 2 == 0`

**Tip:** `%` gives the remainder. A remainder of `0` means the number is divisible by `2`.

---

## Q2. Check Positive, Negative or Zero

```python
num = int(input("Enter the number: "))

if num > 0:
    print("Positive")
elif num < 0:
    print("Negative")
else:
    print("Zero")
```

---

## Q3. Find the Greater of Two Numbers

```python
a = int(input("Enter a value: "))
b = int(input("Enter b value: "))

if a > b:
    print("A is greater")
elif b > a:
    print("B is greater")
else:
    print("Both are equal")
```

**Tip:** Always consider the equality case when comparing two values.

---

## Q4. Check Voting Eligibility

```python
age = int(input("Enter the age: "))

if age >= 18:
    print("The person is eligible to vote")
else:
    print("The person is not eligible to vote")
```

---

## Q5. Check Divisibility by 3

```python
num = int(input("Enter the number: "))

if num % 3 == 0:
    print("The number is divisible by 3")
else:
    print("The number is not divisible by 3")
```

---

## Q6. Check Whether a Number is Between 1 and 100

### Inclusive range: 1 and 100 are included.

```python
num = int(input("Enter the number: "))

if 1 <= num <= 100:
    print("The number is between 1 and 100")
else:
    print("The number is not between 1 and 100")
```

**Tip:**

```python
1 <= num <= 100
```

is equivalent to:

```python
num >= 1 and num <= 100
```

---

## Q7. Check Vowel or Consonant

```python
char = input("Enter one character: ").lower()

if len(char) != 1:
    print("Enter only one character")
elif char in "aeiou":
    print("It is a vowel")
elif char.isalpha():
    print("It is a consonant")
else:
    print("It is not an alphabet")
```

**Tip:** Without validation, entering `@` or `5` could incorrectly be classified as a consonant.

---

## Q8. Check Uppercase or Lowercase

### Comparison-based version

```python
char = input("Enter one character: ")

if len(char) != 1:
    print("Enter only one character")
elif "A" <= char <= "Z":
    print("Uppercase")
elif "a" <= char <= "z":
    print("Lowercase")
else:
    print("Other")
```

### String-method version

```python
char = input("Enter one character: ")

if len(char) != 1:
    print("Enter only one character")
elif char.isupper():
    print("Uppercase")
elif char.islower():
    print("Lowercase")
else:
    print("Other")
```

**Tip:** Use `<=`, not `<`, so `Z` and `z` are included.

---

## Q9. Divisible by 3, 5, Both, or Neither

```python
num = int(input("Enter the number: "))

divisible_by_3 = num % 3 == 0
divisible_by_5 = num % 5 == 0

if divisible_by_3 and divisible_by_5:
    print("Divisible by both 3 and 5")
elif divisible_by_5:
    print("Divisible by 5 only")
elif divisible_by_3:
    print("Divisible by 3 only")
else:
    print("Divisible by neither 3 nor 5")
```

**Tip:** Boolean variables already contain `True` or `False`; you do not need `is True`.

---

## Q10. Leap Year

```python
year = int(input("Enter the year: "))

if year % 400 == 0 or (year % 4 == 0 and year % 100 != 0):
    print(f"{year} is a leap year")
else:
    print(f"{year} is not a leap year")
```

**Examples:**

```text
2000 → Leap year
1900 → Not a leap year
2024 → Leap year
2025 → Not a leap year
```

---

## Q11. Student Grade / Class

```python
total_marks = int(input("Enter total marks: "))
obtained_marks = int(input("Enter obtained marks: "))

if total_marks <= 0:
    print("Total marks must be greater than 0")
elif obtained_marks < 0 or obtained_marks > total_marks:
    print("Invalid obtained marks")
else:
    percentage = (obtained_marks / total_marks) * 100

    print(f"Percentage: {percentage:.2f}%")

    if percentage >= 90:
        print("Distinction")
    elif percentage >= 80:
        print("First Class")
    elif percentage >= 70:
        print("Second Class")
    elif percentage >= 35:
        print("Pass")
    else:
        print("Fail")
```

**Tip:** In descending `elif` logic, once `percentage >= 90` is false, Python already knows the percentage is below `90`. Therefore only the lower boundary is needed in the next condition.

---

## Q12. Check Number of Digits

```python
num = int(input("Enter the number: "))

temp = abs(num)
count = 0

if temp == 0:
    count = 1
else:
    while temp > 0:
        temp //= 10
        count += 1

print("Number of digits:", count)
```

**Tip:** This is the numeric method. It avoids `len(str(num))`.

---

## Q13. Print Numbers from 1 to N

### Using `while`

```python
n = int(input("Enter N: "))

i = 1

while i <= n:
    print(i)
    i += 1
```

### Using `for`

```python
n = int(input("Enter N: "))

for i in range(1, n + 1):
    print(i)
```

---

## Q14. Sum of Numbers from 1 to N

### Loop method

```python
n = int(input("Enter N: "))

total = 0

for i in range(1, n + 1):
    total += i

print("Sum:", total)
```

### Formula

```python
n = int(input("Enter N: "))
print("Sum:", n * (n + 1) // 2)
```

**Tip:** The loop teaches accumulation; the formula is O(1).

---

## Q15. Multiplication Table

```python
num = int(input("Enter the number: "))

for i in range(1, 11):
    print(f"{num} x {i} = {num * i}")
```

---

## Q16. Print Even Numbers from 1 to 100

### Using condition

```python
for i in range(1, 101):
    if i % 2 == 0:
        print(i)
```

### Cleaner version

```python
for i in range(2, 101, 2):
    print(i)
```

---

## Q17. Print Odd Numbers from 1 to 100

```python
for i in range(1, 101, 2):
    print(i)
```

---

## Q18. Print Squares from 1 to 10

```python
for i in range(1, 11):
    print(f"{i}² = {i ** 2}")
```

---

## Q19. Sum of Even Numbers from 1 to N

```python
n = int(input("Enter N: "))

total = 0

for i in range(2, n + 1, 2):
    total += i

print("Sum of even numbers:", total)
```

---

## Q20. Countdown

```python
n = int(input("Enter N: "))

while n > 0:
    print(n)
    n -= 1

print("Done!")
```

---

## Q21. Count Numbers Divisible by 3 from 1 to 100

```python
count = 0

for i in range(3, 101, 3):
    count += 1

print("Count:", count)
```

Output:

```text
33
```

---

## Q22. Password Validation Loop

```python
password = input("Enter password: ")

while password != "aj123":
    print("Wrong password. Try again.")
    password = input("Enter password: ")

print("Login successful!")
```

---

# 🟡 MEDIUM — DIGIT MANIPULATION

> **Core digit pattern:**  
> `% 10` → gets the last digit  
> `// 10` → removes the last digit

---

## Q23. Find the Last Digit of a Number

```python
num = int(input("Enter the number: "))

last_digit = abs(num) % 10

print("Last digit:", last_digit)
```

---

## Q24. Find the First Digit of a Number

```python
num = int(input("Enter the number: "))

temp = abs(num)

while temp >= 10:
    temp //= 10

print("First digit:", temp)
```

**Example:**

```text
58321 → 5
```

---

## Q25. Sum of First and Last Digit

```python
num = int(input("Enter the number: "))

original = abs(num)
temp = original

while temp >= 10:
    temp //= 10

first_digit = temp
last_digit = original % 10

print("Sum of first and last digit:", first_digit + last_digit)
```

---

## Q26. Product of First and Last Digit

```python
num = int(input("Enter the number: "))

original = abs(num)
temp = original

while temp >= 10:
    temp //= 10

first_digit = temp
last_digit = original % 10

print("Product of first and last digit:", first_digit * last_digit)
```

---

## Q27. Sum of Digits

```python
num = int(input("Enter the number: "))

temp = abs(num)
total = 0

while temp > 0:
    digit = temp % 10
    total += digit
    temp //= 10

print("Sum of digits:", total)
```

For `12345`:

```text
1 + 2 + 3 + 4 + 5 = 15
```

---

## Q28. Reverse a Number

```python
num = int(input("Enter the number: "))

original = abs(num)
temp = original
reverse = 0

while temp > 0:
    digit = temp % 10
    reverse = reverse * 10 + digit
    temp //= 10

print("Reverse:", reverse)
```

**Core pattern:**

```python
reverse = reverse * 10 + digit
```

---

## Q29. Find Largest Digit

```python
num = int(input("Enter the number: "))

temp = abs(num)
largest = 0

while temp > 0:
    digit = temp % 10

    if digit > largest:
        largest = digit

    temp //= 10

print("Largest digit:", largest)
```

---

## Q30. Find Smallest Digit

```python
num = int(input("Enter the number: "))

temp = abs(num)
smallest = 9

if temp == 0:
    smallest = 0
else:
    while temp > 0:
        digit = temp % 10

        if digit < smallest:
            smallest = digit

        temp //= 10

print("Smallest digit:", smallest)
```

---

## Q31. Count Even and Odd Digits

```python
num = int(input("Enter the number: "))

temp = abs(num)

even_count = 0
odd_count = 0

if temp == 0:
    even_count = 1
else:
    while temp > 0:
        digit = temp % 10

        if digit % 2 == 0:
            even_count += 1
        else:
            odd_count += 1

        temp //= 10

print("Even digits:", even_count)
print("Odd digits:", odd_count)
```

---

## Q32. Sum of Even Digits

```python
num = int(input("Enter the number: "))

temp = abs(num)
total = 0

while temp > 0:
    digit = temp % 10

    if digit % 2 == 0:
        total += digit

    temp //= 10

print("Sum of even digits:", total)
```

---

## Q33. Sum of Odd Digits

```python
num = int(input("Enter the number: "))

temp = abs(num)
total = 0

while temp > 0:
    digit = temp % 10

    if digit % 2 != 0:
        total += digit

    temp //= 10

print("Sum of odd digits:", total)
```

---

## Q34. Product of Digits

```python
num = int(input("Enter the number: "))

temp = abs(num)
product = 1

if temp == 0:
    product = 0
else:
    while temp > 0:
        digit = temp % 10
        product *= digit
        temp //= 10

print("Product of digits:", product)
```

---

## Q35. Count Zeros in a Number

```python
num = int(input("Enter the number: "))

temp = abs(num)
count = 0

if temp == 0:
    count = 1
else:
    while temp > 0:
        digit = temp % 10

        if digit == 0:
            count += 1

        temp //= 10

print("Number of zeros:", count)
```

---

## Q36. Count a Particular Digit

```python
num = int(input("Enter the number: "))
target = int(input("Enter the digit to count (0-9): "))

if target < 0 or target > 9:
    print("Enter a single digit from 0 to 9")
else:
    temp = abs(num)
    count = 0

    if temp == 0 and target == 0:
        count = 1
    else:
        while temp > 0:
            digit = temp % 10

            if digit == target:
                count += 1

            temp //= 10

    print("Count:", count)
```

---

## Q37. Sum of Odd and Even Numbers from 1 to N

```python
n = int(input("Enter N: "))

even_sum = 0
odd_sum = 0

for i in range(1, n + 1):
    if i % 2 == 0:
        even_sum += i
    else:
        odd_sum += i

print("Even sum:", even_sum)
print("Odd sum:", odd_sum)
```

**Important:** `even_sum += i` adds the actual value.  
`even_count += 1` would only count how many even values exist.

---

## Q38. Count Odd and Even Numbers from 1 to N

```python
n = int(input("Enter N: "))

even_count = 0
odd_count = 0

for i in range(1, n + 1):
    if i % 2 == 0:
        even_count += 1
    else:
        odd_count += 1

print("Even count:", even_count)
print("Odd count:", odd_count)
```

---

## Q39. Average of Numbers from 1 to N

```python
n = int(input("Enter N: "))

total = 0
count = 0

for i in range(1, n + 1):
    total += i
    count += 1

average = total / count

print("Average:", average)
```

---

## Q40. Average of Odd Numbers from 1 to N

```python
n = int(input("Enter N: "))

total = 0
count = 0

for i in range(1, n + 1):
    if i % 2 != 0:
        total += i
        count += 1

if count > 0:
    average = total / count
    print("Average of odd numbers:", average)
else:
    print("No odd numbers in the range")
```

---

# 🟡 MEDIUM — FACTORS, PRIME & NUMBER PROPERTIES

---

## Q41. Find Factors of a Number

```python
num = int(input("Enter a number: "))

for i in range(1, num + 1):
    if num % i == 0:
        print(i, end=" ")
```

Example:

```text
6 → 1 2 3 6
```

---

## Q42. Check Perfect Number

A perfect number equals the sum of its proper divisors.

Example:

```text
6 → 1 + 2 + 3 = 6
```

```python
num = int(input("Enter a number: "))

total = 0

for i in range(1, num):
    if num % i == 0:
        total += i

if num > 0 and total == num:
    print("Perfect number")
else:
    print("Not a perfect number")
```

---

## Q43. Check Prime Number — Basic Factor Count

```python
num = int(input("Enter a number: "))

if num < 2:
    print("Not a prime number")
else:
    count = 0

    for i in range(1, num + 1):
        if num % i == 0:
            count += 1

    if count == 2:
        print("Prime number")
    else:
        print("Not a prime number")
```

---

## Q44. Check Prime Number — `for ... else`

```python
num = int(input("Enter a number: "))

if num < 2:
    print("Not a prime number")
else:
    for i in range(2, num):
        if num % i == 0:
            print("Not a prime number")
            break
    else:
        print("Prime number")
```

**Tip:** The `else` belongs to the `for` loop. It runs only when the loop finishes without `break`.

---

## Q45. Check Prime Number — Optimized

```python
num = int(input("Enter a number: "))

if num < 2:
    print("Not a prime number")
else:
    is_prime = True

    for i in range(2, int(num ** 0.5) + 1):
        if num % i == 0:
            is_prime = False
            break

    if is_prime:
        print("Prime number")
    else:
        print("Not a prime number")
```

**Complexity:** O(√n)

---

## Q46. Print All Prime Numbers from 1 to 100 and Count Them

```python
prime_count = 0

for num in range(2, 101):
    is_prime = True

    for i in range(2, int(num ** 0.5) + 1):
        if num % i == 0:
            is_prime = False
            break

    if is_prime:
        print(num, end=" ")
        prime_count += 1

print()
print("Total primes:", prime_count)
```

Output count:

```text
25
```

---

## Q47. Power Without `**`

```python
base = int(input("Enter the base: "))
power = int(input("Enter the power: "))

if power < 0:
    print("This basic version expects a non-negative power")
else:
    result = 1

    for _ in range(power):
        result *= base

    print("Result:", result)
```

---

## Q48. GCD — Basic Loop

```python
a = int(input("Enter first number: "))
b = int(input("Enter second number: "))

a = abs(a)
b = abs(b)

if a == 0 and b == 0:
    print("GCD is undefined for 0 and 0")
else:
    gcd = 0

    for i in range(1, min(a, b) + 1):
        if a % i == 0 and b % i == 0:
            gcd = i

    if a == 0:
        gcd = b
    elif b == 0:
        gcd = a

    print("GCD:", gcd)
```

---

## Q49. GCD — Euclidean Algorithm

```python
a = int(input("Enter first number: "))
b = int(input("Enter second number: "))

a = abs(a)
b = abs(b)

while b != 0:
    a, b = b, a % b

print("GCD:", a)
```

**Pattern:**

```python
a, b = b, a % b
```

---

## Q50. LCM — Iterative Method

```python
a = int(input("Enter first number: "))
b = int(input("Enter second number: "))

a = abs(a)
b = abs(b)

if a == 0 or b == 0:
    print("LCM: 0")
else:
    lcm = max(a, b)

    while True:
        if lcm % a == 0 and lcm % b == 0:
            break
        lcm += 1

    print("LCM:", lcm)
```

---

## Q51. LCM Using GCD

```python
a = int(input("Enter first number: "))
b = int(input("Enter second number: "))

a = abs(a)
b = abs(b)

if a == 0 or b == 0:
    print("LCM: 0")
else:
    x = a
    y = b

    while y != 0:
        x, y = y, x % y

    gcd = x
    lcm = (a * b) // gcd

    print("LCM:", lcm)
```

Relationship:

```text
LCM × GCD = a × b
```

---

# 🟠 MEDIUM-HARD — FIBONACCI & PALINDROME

---

## Q52. Fibonacci Series

Print the first N Fibonacci terms.

```python
n = int(input("Enter N: "))

a = 0
b = 1

for _ in range(n):
    print(a, end=" ")
    a, b = b, a + b
```

Example for `7`:

```text
0 1 1 2 3 5 8
```

---

## Q53. Check Whether a Number Belongs to Fibonacci Series

```python
n = int(input("Enter the number: "))

if n < 0:
    print("No")
else:
    a = 0
    b = 1

    while a < n:
        a, b = b, a + b

    if a == n:
        print("Yes, it belongs to the Fibonacci series")
    else:
        print("No, it does not belong to the Fibonacci series")
```

---

## Q54. Palindrome Number

### Numeric method — preferred for number practice

```python
num = int(input("Enter a number: "))

original = abs(num)
temp = original
reverse = 0

while temp > 0:
    digit = temp % 10
    reverse = reverse * 10 + digit
    temp //= 10

if original == reverse:
    print("Palindrome number")
else:
    print("Not a palindrome number")
```

---

## Q55. Sum of Digits Until One Digit Remains

Example:

```text
9875
9+8+7+5 = 29
2+9 = 11
1+1 = 2
```

```python
num = int(input("Enter a number: "))

num = abs(num)

while num >= 10:
    total = 0

    while num > 0:
        digit = num % 10
        total += digit
        num //= 10

    num = total

print("Single digit:", num)
```

---

# 🔴 HARD — SPECIAL NUMBER PROBLEMS

---

## Q56. Armstrong Number

A number is Armstrong if the sum of each digit raised to the number of digits equals the original number.

Example:

```text
153 = 1³ + 5³ + 3³
    = 1 + 125 + 27
    = 153
```

```python
num = int(input("Enter a number: "))

if num < 0:
    print("Negative numbers are not handled in this basic version")
else:
    original = num
    temp = num
    digits = 1 if num == 0 else 0

    if num != 0:
        while temp > 0:
            digits += 1
            temp //= 10

    temp = num
    total = 0

    while temp > 0:
        digit = temp % 10
        total += digit ** digits
        temp //= 10

    if original == total:
        print("Armstrong number")
    else:
        print("Not an Armstrong number")
```

**Important corrections from the original practice:**

Wrong:

```python
while temp <= 0:
```

Correct:

```python
while temp > 0:
```

Wrong:

```python
temp == num // 10
```

Correct:

```python
temp = num // 10
```

`=` means assignment.  
`==` means comparison.

---

## Q57. Strong Number

A strong number equals the sum of the factorials of its digits.

Example:

```text
145 = 1! + 4! + 5!
    = 1 + 24 + 120
    = 145
```

```python
import math

num = int(input("Enter a number: "))

original = num
temp = abs(num)
total = 0

if temp == 0:
    total = math.factorial(0)
else:
    while temp > 0:
        digit = temp % 10
        total += math.factorial(digit)
        temp //= 10

if original >= 0 and original == total:
    print("Strong number")
else:
    print("Not a strong number")
```

**Important:** Each digit needs its own factorial. Do not reuse one accumulated `fact` across digits.

---

## Q58. Second Largest Distinct Digit

```python
num = int(input("Enter a number: "))

temp = abs(num)

largest = -1
second_largest = -1

while temp > 0:
    digit = temp % 10

    if digit > largest:
        second_largest = largest
        largest = digit
    elif digit > second_largest and digit != largest:
        second_largest = digit

    temp //= 10

if second_largest == -1:
    print("There is no second distinct largest digit")
else:
    print("Second largest digit:", second_largest)
```

---

## Q59. Harshad / Niven Number

A number is a Harshad number if it is divisible by the sum of its digits.

```python
num = int(input("Enter a number: "))

if num <= 0:
    print("Enter a positive number")
else:
    original = num
    digit_sum = 0

    while num > 0:
        digit_sum += num % 10
        num //= 10

    if original % digit_sum == 0:
        print("Harshad number")
    else:
        print("Not a Harshad number")
```

Example:

```text
18 → 1 + 8 = 9
18 % 9 = 0
```

---

## Q60. Extract Even Digits and Form a Number

```python
num = int(input("Enter a number: "))

temp = abs(num)
result = 0
place = 1

while temp > 0:
    digit = temp % 10

    if digit % 2 == 0:
        result += digit * place
        place *= 10

    temp //= 10

print("Even digits number:", result)
```

Example:

```text
123456 → 246
```

---

# 🔴 HARD — NESTED CONDITIONS & VALIDATION

---

## Q61. Calculator Using Conditions

```python
a = int(input("Enter the first number: "))
b = int(input("Enter the second number: "))
operator = input("Enter the operator: ")

if operator == "+":
    print(f"{a} + {b} = {a + b}")

elif operator == "-":
    print(f"{a} - {b} = {a - b}")

elif operator == "*":
    print(f"{a} * {b} = {a * b}")

elif operator == "**":
    print(f"{a} ** {b} = {a ** b}")

elif operator == "/":
    if b == 0:
        print("Cannot divide by zero")
    else:
        print(f"{a} / {b} = {a / b}")

elif operator == "//":
    if b == 0:
        print("Cannot divide by zero")
    else:
        print(f"{a} // {b} = {a // b}")

elif operator == "%":
    if b == 0:
        print("Cannot divide by zero")
    else:
        print(f"{a} % {b} = {a % b}")

else:
    print("Enter a valid operator")
```

---

## Q62. Login System

```python
username = input("Enter the username: ")
password = int(input("Enter the password: "))

correct_username = "Gagan_a_j"
correct_password = 4522

if username == correct_username:
    if password == correct_password:
        print("Login successful")
    else:
        print("Incorrect password")
else:
    print("Incorrect username")
```

**Pattern:** This is an example of nested `if`.

---

## Q63. Banking System

```python
account_num = 123456789
correct_pin = 4522
balance = 50000

acc_num = int(input("Enter account number: "))
pin = int(input("Enter PIN: "))
amount = int(input("Enter amount to withdraw: "))

if acc_num == account_num:
    if pin == correct_pin:

        if amount <= 0:
            print("Invalid withdrawal amount")

        elif amount > balance:
            print("Insufficient balance")

        else:
            balance -= amount
            print(f"Successfully withdrawn ₹{amount}")
            print(f"Remaining balance: ₹{balance}")

    else:
        print("Incorrect PIN")
else:
    print("Incorrect account number")
```

**Important edge case:** A negative withdrawal amount must not increase the balance.

---

## Q64. Largest of Three Numbers

```python
a = int(input("Enter the a value: "))
b = int(input("Enter the b value: "))
c = int(input("Enter the c value: "))

if a > b and a > c:
    print("A is greater")

elif b > a and b > c:
    print("B is greater")

elif c > a and c > b:
    print("C is greater")

else:
    print("There is a tie")
```

**Important correction:** Remove unnecessary:

```python
if True:
```

Also note that `c < a > b` is valid Python, but writing:

```python
a > b and a > c
```

is clearer.

---

## Q65. Valid Date Checker

```python
day = int(input("Enter the day: "))
month = int(input("Enter the month: "))
year = int(input("Enter the year: "))

is_leap = (year % 400 == 0) or (year % 4 == 0 and year % 100 != 0)

if year <= 0:
    print("Invalid year")

elif month < 1 or month > 12:
    print("Invalid month")

elif day < 1:
    print("Invalid day")

elif month in [1, 3, 5, 7, 8, 10, 12]:
    if day <= 31:
        print("Valid date")
    else:
        print("Invalid date")

elif month in [4, 6, 9, 11]:
    if day <= 30:
        print("Valid date")
    else:
        print("Invalid date")

elif month == 2:
    if is_leap:
        if day <= 29:
            print("Valid date")
        else:
            print("Invalid date")
    else:
        if day <= 28:
            print("Valid date")
        else:
            print("Invalid date")
```

**Important correction:** In a non-leap year, February allows `1–28`, not `1–27`.

---

# 🟡 STRING BASICS

> These are separate from numeric digit manipulation.

---

## Q66. Find a String

```python
text = "gagajkamk"

print(text.find("l", 6, 9))
```

If the substring is not found, `find()` returns:

```text
-1
```

---

## Q67. Use `index()`

```python
text = "gagajkamk"

print(text.index("l", 6, 9))
```

If the substring is not found, `index()` raises a `ValueError`.

### Difference

| Method | Not found |
|---|---|
| `find()` | `-1` |
| `index()` | `ValueError` |

---

## Q68. `split()` a String

```python
text = "Apple,Banana,Mango,Orange"

fruits = text.split(",")

print(fruits)
```

Output:

```text
['Apple', 'Banana', 'Mango', 'Orange']
```

---

## Q69. `join()` a List

```python
fruits = ["Apple", "Banana", "Mango"]

print(",".join(fruits))
print("-".join(fruits))
```

---

## Q70. Chain String Methods

```python
text = "   I am a Python program.   "

result = text.strip().upper()

print(result)
```

**Tip:** Each method operates on the result returned by the previous method. Check the intermediate result when debugging a chain.

---

## Q71. Vowel Count in a String

```python
text = input("Enter a sentence: ").lower()

count = 0

for char in text:
    if char in "aeiou":
        count += 1

print("Vowel count:", count)
```

---

## Q72. Palindrome String

```python
text = input("Enter a string: ").lower().replace(" ", "")

if text == text[::-1]:
    print("Palindrome")
else:
    print("Not a palindrome")
```

---

## Q73. Word Count in a Sentence

```python
text = input("Enter a sentence: ")

words = text.split()

print("Word count:", len(words))
```

---

## Q74. Longest Word in a Sentence

```python
text = input("Enter a sentence: ")

words = text.split()

if words:
    longest = max(words, key=len)
    print("Longest word:", longest)
else:
    print("No words entered")
```

---

## Q75. Character Frequency

```python
word = input("Enter a word: ")

for char in sorted(set(word)):
    print(f"'{char}': {word.count(char)}")
```

---

## Q76. Reverse a String Using a Loop

```python
text = input("Enter a string: ")

reverse = ""

for i in range(len(text) - 1, -1, -1):
    reverse += text[i]

print("Reverse:", reverse)
```

---

## Q77. Reverse Words in a Sentence

```python
text = input("Enter a sentence: ")

words = text.split()

reversed_words = words[::-1]

print(" ".join(reversed_words))
```

---

# 🔴 PATTERN PROGRAMS — NESTED LOOPS

---

## P1. Square Pattern

```text
* * * * *
* * * * *
* * * * *
* * * * *
* * * * *
```

```python
n = int(input("Enter N: "))

for row in range(n):
    for col in range(n):
        print("*", end=" ")
    print()
```

---

## P2. Right Triangle — Increasing

```text
*
* *
* * *
* * * *
* * * * *
```

```python
n = int(input("Enter N: "))

for row in range(1, n + 1):
    for col in range(row):
        print("*", end=" ")
    print()
```

---

## P3. Right Triangle — Decreasing

```text
* * * * *
* * * *
* * *
* *
*
```

```python
n = int(input("Enter N: "))

for row in range(n, 0, -1):
    for col in range(row):
        print("*", end=" ")
    print()
```

---

## P4. Number Triangle

```text
1
1 2
1 2 3
1 2 3 4
1 2 3 4 5
```

```python
n = int(input("Enter N: "))

for row in range(1, n + 1):
    for col in range(1, row + 1):
        print(col, end=" ")
    print()
```

---

## P5. Inverted Number Triangle

```text
5 4 3 2 1
5 4 3 2
5 4 3
5 4
5
```

```python
n = int(input("Enter N: "))

for row in range(n, 0, -1):
    for col in range(n, n - row, -1):
        print(col, end=" ")
    print()
```

---

## P6. Right-Aligned Pyramid

```text
        *
      * *
    * * *
  * * * *
* * * * *
```

```python
n = int(input("Enter N: "))

for row in range(1, n + 1):
    for space in range(n - row):
        print(" ", end=" ")

    for col in range(row):
        print("*", end=" ")

    print()
```

---

## P7. Alternating 1 2 Triangle

```text
        1
      1 2
    1 2 1
  1 2 1 2
1 2 1 2 1
```

```python
n = int(input("Enter N: "))

for row in range(1, n + 1):
    for space in range(n - row):
        print(" ", end=" ")

    for col in range(1, row + 1):
        if col % 2 != 0:
            print("1", end=" ")
        else:
            print("2", end=" ")

    print()
```

---

# 🔴 BASIC DSA / ARRAY PRACTICE

---

## Q78. Find Maximum in an Array

```python
arr = [50, 25, 7, 60, 15]

maximum = arr[0]

for num in arr:
    if num > maximum:
        maximum = num

print("Maximum:", maximum)
```

**Tip:** Starting from `arr[0]` works even when every number is negative.

---

## Q79. Linear Search

```python
arr = [50, 25, 7, 60, 15]
target = 60

found = False

for i in range(len(arr)):
    if arr[i] == target:
        print(f"{target} found at index {i}")
        found = True
        break

if not found:
    print(f"{target} not found")
```

**Complexity:** O(n)

---

## Q80. Two Sum — Brute Force

```python
arr = [2, 7, 4, 3, 11, 6]
target = 10

found = False

for i in range(len(arr)):
    for j in range(i + 1, len(arr)):
        if arr[i] + arr[j] == target:
            print(f"Pair found: {arr[i]} + {arr[j]} = {target}")
            print(f"Indices: {i} and {j}")
            found = True
            break

    if found:
        break

if not found:
    print("No pair found")
```

**Complexity:** O(n²)

---

## Q81. Two Sum — Hash Set

```python
arr = [2, 7, 4, 3, 11, 6]
target = 10

seen = set()

for num in arr:
    complement = target - num

    if complement in seen:
        print(f"Pair: {complement} + {num} = {target}")
        break

    seen.add(num)
```

**Average time complexity:** O(n)

---

# 🔴 ADVANCED PRIME GENERATION

---

## Q82. Sieve of Eratosthenes

Find all primes from 1 to N efficiently.

```python
n = int(input("Enter N: "))

if n < 2:
    print([])
else:
    is_prime = [True] * (n + 1)

    is_prime[0] = False
    is_prime[1] = False

    for i in range(2, int(n ** 0.5) + 1):
        if is_prime[i]:
            for j in range(i * i, n + 1, i):
                is_prime[j] = False

    primes = []

    for i in range(2, n + 1):
        if is_prime[i]:
            primes.append(i)

    print(primes)
    print("Count:", len(primes))
```

---

# QUICK REFERENCE — CORE PATTERNS

```python
# -----------------------------
# CONDITIONS
# -----------------------------

if condition:
    ...
elif condition:
    ...
else:
    ...


# -----------------------------
# LAST DIGIT
# -----------------------------

digit = num % 10


# -----------------------------
# REMOVE LAST DIGIT
# -----------------------------

num //= 10


# -----------------------------
# FIRST DIGIT
# -----------------------------

temp = abs(num)

while temp >= 10:
    temp //= 10

first_digit = temp


# -----------------------------
# DIGIT LOOP
# -----------------------------

temp = abs(num)

while temp > 0:
    digit = temp % 10

    # process digit here

    temp //= 10


# -----------------------------
# COUNT DIGITS
# -----------------------------

count = 0

while num > 0:
    num //= 10
    count += 1


# -----------------------------
# SUM OF DIGITS
# -----------------------------

total = 0

while num > 0:
    digit = num % 10
    total += digit
    num //= 10


# -----------------------------
# REVERSE NUMBER
# -----------------------------

reverse = 0

while num > 0:
    digit = num % 10
    reverse = reverse * 10 + digit
    num //= 10


# -----------------------------
# LARGEST DIGIT
# -----------------------------

largest = 0

if digit > largest:
    largest = digit


# -----------------------------
# SMALLEST DIGIT
# -----------------------------

smallest = 9

if digit < smallest:
    smallest = digit


# -----------------------------
# PRIME — O(sqrt(n))
# -----------------------------

for i in range(2, int(num ** 0.5) + 1):
    if num % i == 0:
        ...


# -----------------------------
# GCD — EUCLIDEAN ALGORITHM
# -----------------------------

while b:
    a, b = b, a % b


# -----------------------------
# LCM USING GCD
# -----------------------------

lcm = (a * b) // gcd


# -----------------------------
# FIBONACCI
# -----------------------------

a, b = b, a + b


# -----------------------------
# POWER WITHOUT **
# -----------------------------

result = 1

for _ in range(power):
    result *= base


# -----------------------------
# FACTORIAL
# -----------------------------

fact = 1

for i in range(1, n + 1):
    fact *= i
```

---

# COMMON MISTAKES TO REMEMBER

## 1. `=` vs `==`

Wrong:

```python
temp == num // 10
```

Correct:

```python
temp = num // 10
```

`=` → assignment  
`==` → comparison

---

## 2. `<` vs `<=`

Wrong for an inclusive 1–100 range:

```python
num > 0 and num < 100
```

Correct:

```python
1 <= num <= 100
```

---

## 3. Count vs Sum

Count:

```python
even_count += 1
```

Sum:

```python
even_sum += i
```

Do not confuse them.

---

## 4. Missing Cases

If the possible outcomes are:

```text
both
3 only
5 only
neither
```

write all four cases.

---

## 5. Equality Case

For two numbers:

```python
if a > b:
    ...
elif b > a:
    ...
else:
    # equal
```

---

## 6. Wrong Loop Condition

For digit processing:

```python
while temp > 0:
```

not:

```python
while temp <= 0:
```

for normal positive input.

---

## 7. Forgetting to Update the Loop Variable

This causes an infinite loop:

```python
i = 1

while i <= 10:
    print(i)
```

Correct:

```python
i = 1

while i <= 10:
    print(i)
    i += 1
```

---

## 8. Wrong Variable in Nested Loops

Wrong:

```python
for j in range(...):
    if b % i == 0:
        ...
```

when the divisor variable is actually `j`.

Correct:

```python
for j in range(...):
    if b % j == 0:
        ...
```

---

## 9. Reset Values That Belong to Each Digit

In Strong Number, factorial must be calculated independently for every digit.

Do not keep one accumulated factorial for all digits.

---

## 10. Do Not Use String Conversion Just to Avoid Numeric Logic

For learning number manipulation, prefer:

```python
digit = num % 10
num //= 10
```

rather than:

```python
num = input(...)
num[0]
num[-1]
```

The numeric approach is the main pattern being practiced here.

---

# TOPIC MAP

| Topic | Main concept |
|---|---|
| Even/Odd | `%` |
| Positive/Negative | Comparison |
| Greater of two/three | Comparison + `and` |
| Leap year | `and` / `or` + `%` |
| Voting | Comparison |
| Range | Chained comparison |
| Grade | `if / elif / else` |
| Divisibility | `%` |
| Vowel | `in` |
| Upper/Lower | Character comparison / methods |
| Multiplication table | Loop |
| 1 to N | Loop |
| Sum 1 to N | Accumulator |
| Count digits | `% 10` + `// 10` |
| First digit | Repeated `// 10` |
| Last digit | `% 10` |
| Sum digits | Accumulator + digit extraction |
| Reverse | `reverse * 10 + digit` |
| Largest/smallest digit | Comparison + digit extraction |
| Even/odd digit count | Condition + counter |
| Factors | `%` + loop |
| Prime | Factors + `break` |
| Perfect number | Sum of divisors |
| GCD | Euclidean algorithm |
| LCM | Multiples / GCD |
| Fibonacci | Previous two values |
| Palindrome | Reverse + compare |
| Armstrong | Powers of digits |
| Strong number | Factorial of digits |
| Harshad | Digit sum + divisibility |
| Valid date | Nested conditions |
| Calculator | `if / elif / else` |
| Login | Nested `if` |
| Banking | Nested `if` + validation |
| Strings | `find`, `index`, `split`, `join` |
| Patterns | Nested loops |
| Arrays | Iteration |
| Two Sum | Nested loop / set |
| Sieve | Boolean array + nested loops |

---

# FINAL REVISION ORDER

### 🟢 EASY
1. Even / Odd
2. Positive / Negative / Zero
3. Greater of two
4. Voting eligibility
5. Divisible by 3
6. Range 1–100
7. Vowel / consonant
8. Uppercase / lowercase
9. Divisible by 3 / 5 / both / neither
10. Leap year
11. Grade
12. Print 1 to N
13. Sum 1 to N
14. Multiplication table
15. Even / odd numbers
16. Squares
17. Countdown

### 🟡 MEDIUM
18. Count digits
19. Last digit
20. First digit
21. First + last
22. First × last
23. Sum digits
24. Reverse number
25. Largest digit
26. Smallest digit
27. Even/odd digit count
28. Sum even/odd digits
29. Product digits
30. Count zeros
31. Count particular digit
32. Factors
33. Prime
34. Count/print primes
35. Perfect number
36. Power
37. Average
38. GCD
39. LCM
40. Fibonacci
41. Fibonacci membership
42. Palindrome

### 🟠 MEDIUM-HARD
43. Sum until one digit
44. Armstrong
45. Strong number
46. Harshad number

### 🔴 HARD
47. Second largest digit
48. Extract even digits
49. Calculator
50. Login
51. Banking
52. Valid date
53. Array maximum
54. Linear search
55. Two Sum
56. Sieve of Eratosthenes
57. Pattern programs
58. String problems

