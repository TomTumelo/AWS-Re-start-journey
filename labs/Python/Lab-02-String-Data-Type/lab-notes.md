# Lab Notes: Working with the String Data Type

**Date Completed:** <!-- Add your date -->
**Duration:** ~45 minutes
**Environment:** AWS Cloud9 (reStart-python-cloud9)
**File:** string-data-type.py

---

## Exercise 1 - Introducing the String Data Type

myString = "This is a string."
print(myString)
print(type(myString))
print(myString + " is of the data type " + str(type(myString)))

Output:
This is a string.
class str
This is a string. is of the data type class str

---

## Exercise 2 - String Concatenation

The + operator combines strings. When used with strings it joins them, unlike with numbers where it adds them.

firstString = "water"
secondString = "fall"
thirdString = firstString + secondString
print(thirdString)

Output:
waterfall

---

## Exercise 3 - Working with Input Strings

Used the input() function to accept user input. The function pauses the script until the user types something and presses ENTER.

name = input("What is your name? ")
print(name)

Output:
What is your name? Tumelo
Tumelo

---

## Exercise 4 - Formatting Output Strings

Used the format() function to insert multiple variables into a single output string. Curly braces act as placeholders.

color = input("What is your favorite color? ")
animal = input("What is your favorite animal? ")
print("{}, you like a {} {}!".format(name,color,animal))

Output:
What is your favorite color? Blue
What is your favorite animal? cat
Tumelo, you like a Blue cat!

---

## Screenshot

- screenshots/code-and-output.png - Full code and console output in Cloud9

---

## Key Lessons Learned

**Strings**
- A string is any collection of letters, numbers, and symbols wrapped in quotes
- Use type() to confirm the data type is str
- Use str() to convert other data types to strings for concatenation

**Concatenation**
- The + operator joins strings together
- "water" + "fall" produces "waterfall" with no space
- To add a space between words use a space string as a separator

**Input**
- input() pauses the script and waits for the user to type something
- Whatever the user types is stored as a string automatically

**String Formatting**
- format() is a cleaner way to build output strings with multiple variables
- Curly braces act as placeholders in the order the variables are passed
- Much more readable than chaining + operators together
