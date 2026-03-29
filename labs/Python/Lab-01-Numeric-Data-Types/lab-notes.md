# Lab Notes: Working with Numeric Data Types

**Date Completed:** <!-- Add your date -->
**Duration:** ~60 minutes
**Environment:** AWS Cloud9 (reStart-python-cloud9)
**File:** numeric-data.py

---

## Environment Setup

Accessed the lab through the AWS Management Console, navigated to Cloud9 via Services, and opened the reStart-python-cloud9 environment. Created a new Python file called numeric-data.py in the /home/ec2-user/environment directory.

---

## Exercise 1 - Using the Python Shell

Opened the Python shell directly in the Cloud9 terminal:

```bash
python3
```

Tested basic arithmetic operations:

```python
>>> 2 + 2
4
>>> 4 - 2
2
>>> 4 / 2
2.0
>>> quit()
```

Key observation: Division always returns a float (2.0 not 2).

---

## Exercise 2 - The int Data Type

```python
myValue=1
print(myValue)
print(type(myValue))
print(str(myValue) + " is of the data type " + str(type(myValue)))
```

Output:
```
1
<class int>
1 is of the data type <class int>
```

---

## Exercise 3 - The float Data Type

```python
myValue=3.14
print(myValue)
print(type(myValue))
print(str(myValue) + " is of the data type " + str(type(myValue)))
```

Output:
```
3.14
<class float>
3.14 is of the data type <class float>
```

---

## Exercise 4 - The complex Data Type

```python
myValue=5j
print(myValue)
print(type(myValue))
print(str(myValue) + " is of the data type " + str(type(myValue)))
```

Output:
```
5j
<class complex>
5j is of the data type <class complex>
```

---

## Exercise 5 - The bool Data Type

```python
myValue=True
print(myValue)
print(type(myValue))
print(str(myValue) + " is of the data type " + str(type(myValue)))

myValue=False
print(myValue)
print(type(myValue))
print(str(myValue) + " is of the data type " + str(type(myValue)))
```

Output:
```
True
<class bool>
True is of the data type <class bool>
False
<class bool>
False is of the data type <class bool>
```

---

## Screenshots

- screenshots/code.png - Full numeric-data.py code in Cloud9 editor
- screenshots/output.png - Complete console output showing all data types

---

## Key Lessons Learned

**Python numeric data types**
- int stores whole numbers like 1, 42, 100
- float stores decimal numbers like 3.14
- complex stores imaginary numbers like 5j used in advanced math
- bool is technically a subset of int where True equals 1 and False equals 0

**Built-in functions used**
- print() writes output to the console
- type() returns the data type of a variable
- str() converts a value to a string for concatenation

**Cloud9 as a dev environment**
- AWS Cloud9 runs in the browser with no local setup needed
- Files live at /home/ec2-user/environment
- The environment resets after the session ends so always save your code externally
