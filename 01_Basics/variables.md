# Understanding Variables in Python

Variables are fundamental to any programming language. They act as containers or labels for storing data values. In Python, you can think of a variable as a name pointing to a specific location in the computer's memory where a value is stored.

---

## 1. Declaring and Assigning Variables

Python is a dynamically-typed language, which means you don't need to explicitly declare the type of a variable. The type is inferred at runtime based on the value you assign to it.

To create a variable, you just need to specify its name and assign a value to it using the equals sign (`=`).

```python
# Assigning an integer
age = 30

# Assigning a string
name = "Alice"

# Assigning a float (a number with a decimal)
height = 5.8

# Assigning a boolean (True or False)
is_student = False

print(name)       # Output: Alice
print(age)        # Output: 30
print(height)     # Output: 5.8
print(is_student) # Output: False
```

### Re-assigning Variables

You can change the value of a variable at any time. You can even change its type.

```python
x = 100
print(x)  # Output: 100

# Re-assigning x to a new value
x = 200
print(x)  # Output: 200

# Re-assigning x to a different data type
x = "Hello, Python!"
print(x)  # Output: Hello, Python!
```

---

## 2. Naming Conventions

Choosing good variable names is crucial for writing readable and maintainable code. Python has a set of rules and conventions for naming variables:

### Rules (Must be followed):

1.  A variable name must start with a letter (`a-z`, `A-Z`) or an underscore (`_`).
2.  It cannot start with a number.
3.  It can only contain alpha-numeric characters and underscores (`A-z`, `0-9`, and `_`).
4.  Variable names are case-sensitive (`age`, `Age`, and `AGE` are three different variables).

```python
# Legal variable names
my_variable = "Correct"
_another_variable = "Also Correct"
variable2 = "And this one too"

# Illegal variable names
# 2variable = "Starts with a number"
# my-variable = "Contains a hyphen"
# my variable = "Contains a space"
```

### Conventions (Should be followed for good practice):

Python's official style guide, PEP 8, recommends using **snake_case** for variable names. This means all letters are lowercase, and words are separated by underscores.

```python
# Good (snake_case)
first_name = "John"
user_email_address = "john.doe@example.com"

# Bad (camelCase or PascalCase - common in other languages)
# firstName = "John"
# UserEmailAddress = "john.doe@example.com"
```

---

## 3. Multiple Assignment

Python allows you to assign values to multiple variables in a single line, which can be very convenient.

### Assigning the same value to multiple variables:

```python
a = b = c = 10
print(a)  # Output: 10
print(b)  # Output: 10
print(c)  # Output: 10
```

### Assigning different values to multiple variables:

This is often called "unpacking."

```python
x, y, z = "Apple", "Banana", "Cherry"
print(x)  # Output: Apple
print(y)  # Output: Banana
print(z)  # Output: Cherry
```

This is a powerful feature, often used to swap the values of two variables without needing a temporary variable:

```python
a = 5
b = 10

# Swap the values
a, b = b, a

print(a)  # Output: 10
print(b)  # Output: 5
```
