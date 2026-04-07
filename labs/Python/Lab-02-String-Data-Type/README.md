# 🐍 Lab 10 — Python: String Data Type

> **Domain:** Python | **Status:** ✅ Complete

---

## 🎯 Lab Objective

Master Python string manipulation — one of the most essential skills for scripting, automation, and working with AWS CLI outputs, log files, and API responses.

---

## 📚 What I Did

Completed exercises covering string creation, indexing, slicing, methods, and formatting.

---

## 🧠 Key Concepts Covered

### Creating Strings
```python
single = 'Hello, AWS!'
double = "re/Start Journey"
multi  = """This is a
multi-line string"""

# Escape characters
path   = "C:\\Users\\Tumelo"   # Backslash
tab    = "Column1\tColumn2"    # Tab
newline = "Line1\nLine2"       # Newline
```

### String Indexing & Slicing
```python
s = "CloudPractitioner"
#    0123456789...

s[0]        # 'C'         → First character
s[-1]       # 'r'         → Last character
s[0:5]      # 'Cloud'     → Slice [start:end] (end not included)
s[5:]       # 'Practitioner' → From index 5 to end
s[:5]       # 'Cloud'     → From start to index 5
s[::2]      # Every second character
s[::-1]     # 'renoitatcitcarPduolC' → Reverse the string
```

### Essential String Methods
```python
text = "  aws restart program  "

# Case
text.upper()          # "  AWS RESTART PROGRAM  "
text.lower()          # "  aws restart program  "
text.title()          # "  Aws Restart Program  "
text.capitalize()     # "  aws restart program  "

# Whitespace
text.strip()          # "aws restart program"
text.lstrip()         # "aws restart program  "
text.rstrip()         # "  aws restart program"

# Search & Replace
text.find("restart")  # Returns index of first match (-1 if not found)
text.replace("aws", "AWS")  # "  AWS restart program  "
"restart" in text     # True → membership test

# Split & Join
csv = "EC2,S3,RDS,Lambda"
services = csv.split(",")   # ['EC2', 'S3', 'RDS', 'Lambda']
"-".join(services)          # 'EC2-S3-RDS-Lambda'

# Check content
"123".isdigit()       # True
"abc".isalpha()       # True
"".isspace() or ""    # Careful with empty string checks
text.startswith("  aws")    # True
text.endswith("  ")         # True
```

### String Formatting
```python
name = "Tumelo"
service = "EC2"
cost = 8.352

# f-strings (recommended — Python 3.6+)
print(f"Hello, {name}! Your {service} costs ${cost:.2f}/month")
# Hello, Tumelo! Your EC2 costs $8.35/month

# .format() method
print("Hello, {}! Your {} costs ${:.2f}/month".format(name, service, cost))

# % formatting (older style)
print("Hello, %s!" % name)
```

### Real-World Example: Parsing AWS Output
```python
# Parsing an EC2 instance ID from a string
output = "InstanceId: i-0abc123def456789a, State: running"

# Extract instance ID
start = output.find("i-")
instance_id = output[start:start+19]
print(instance_id)  # i-0abc123def456789a

# Or using split
parts = output.split(", ")
for part in parts:
    if "InstanceId" in part:
        id_part = part.split(": ")[1]
        print(id_part)  # i-0abc123def456789a
```

---

## 💡 Key Takeaways

1. **Strings are immutable** — methods return new strings, they don't modify in place.
2. **`strip()` before processing** — user input and file lines often have hidden whitespace.
3. **`in` operator is the cleanest membership test** — `if "error" in log_line:` is Pythonic.
4. **f-strings are the modern standard** — more readable than `%` or `.format()`.
5. **`split()` and `join()` are inverses** — master both and you can parse almost any text format.

---

## 📸 Screenshots

> Screenshots available in [`./screenshots/`](./screenshots/)
