# 🐍 Lab 09 — Python: Numeric Data Types

> **Domain:** Python | **Status:** ✅ Complete

---

## 🎯 Lab Objective

Explore Python's numeric data types — integers, floats, and complex numbers. Practice arithmetic operations, type conversion, and built-in math functions through 8 hands-on exercises.

---

## 📚 What I Did

Completed **8 exercises** covering numeric types, operations, and output formatting.

### Exercises Completed

| Exercise | Topic |
|---|---|
| 1 | Integer and float variable declaration |
| 2 | Basic arithmetic operators (+, -, *, /) |
| 3 | Integer division (`//`) and modulo (`%`) |
| 4 | Exponentiation (`**`) |
| 5 | Type conversion (`int()`, `float()`, `str()`) |
| 6 | Built-in math functions (`abs()`, `round()`, `pow()`) |
| 7 | The `math` module (`math.sqrt()`, `math.pi`, `math.ceil()`) |
| 8 | Combining numeric operations in a real-world calculation |

---

## 🧠 Key Concepts Covered

### Python Numeric Types
```python
# Integer (whole numbers, no decimal point)
age = 25
year = 2026
negative = -10

# Float (decimal point numbers)
price = 99.99
temperature = 36.6
pi_approx = 3.14

# Complex (real + imaginary — less common)
z = 3 + 4j
```

### Arithmetic Operators
```python
a, b = 10, 3

print(a + b)    # 13  → Addition
print(a - b)    # 7   → Subtraction
print(a * b)    # 30  → Multiplication
print(a / b)    # 3.3333... → True division (always float)
print(a // b)   # 3   → Floor division (integer result)
print(a % b)    # 1   → Modulo (remainder)
print(a ** b)   # 1000 → Exponentiation
```

### Type Conversion
```python
x = "42"
y = int(x)        # "42" → 42 (string to int)
z = float(y)      # 42 → 42.0 (int to float)
s = str(z)        # 42.0 → "42.0" (float to string)

# Common pitfall
result = "5" + 3  # ❌ TypeError! Can't add str and int
result = int("5") + 3  # ✅ 8
```

### Built-in Math Functions
```python
abs(-15)          # 15  → Absolute value
round(3.14159, 2) # 3.14 → Round to 2 decimal places
pow(2, 8)         # 256 → Same as 2**8
max(1, 5, 3)      # 5
min(1, 5, 3)      # 1
```

### The `math` Module
```python
import math

math.sqrt(144)    # 12.0
math.pi           # 3.141592653589793
math.ceil(4.1)    # 5  → Round up
math.floor(4.9)   # 4  → Round down
math.log(100, 10) # 2.0 → Log base 10
```

### Real-World Example: AWS Cost Calculator
```python
# Calculate monthly EC2 cost
hourly_rate = 0.0116       # t3.micro in USD
hours_per_day = 24
days_per_month = 30

monthly_cost = hourly_rate * hours_per_day * days_per_month
print(f"Monthly cost: ${monthly_cost:.2f}")
# Monthly cost: $8.35
```

---

## 💡 Key Takeaways

1. **`/` always returns a float in Python 3** — use `//` when you need integer division.
2. **Type matters** — `"5" + 3` crashes, `int("5") + 3` works. Always be aware of types.
3. **`round()` uses banker's rounding** — `round(0.5)` = 0, `round(1.5)` = 2. Use `math.ceil/floor` for predictable rounding.
4. **`f-strings` are the cleanest way to format numbers** — `f"{price:.2f}"` for currency.
5. **Import `math` for anything beyond basic arithmetic** — square roots, logs, trig, constants.

---

## 📸 Screenshots

> Screenshots available in [`./screenshots/`](./screenshots/)
