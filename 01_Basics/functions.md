# Functions in Python

A function is a block of organized, reusable code that is used to perform a single, related action. Functions provide better modularity for your application and a high degree of code reusing.

---

## 1. Defining and Calling a Function

You define a function using the `def` keyword, followed by a function name, parentheses `()`, and a colon `:`. The code block within every function starts with an indentation.

To call a function, you use the function name followed by parentheses.

```python
# Defining a simple function
def greet():
    print("Hello, World!")

# Calling the function
greet()  # Output: Hello, World!
```

---

## 2. Arguments and Parameters

Information can be passed into functions as arguments. Arguments are specified after the function name, inside the parentheses. You can add as many arguments as you want, just separate them with a comma.

-   A **parameter** is the variable listed inside the parentheses in the function definition.
-   An **argument** is the value that is sent to the function when it is called.

```python
def greet_user(name):  # 'name' is a parameter
    print(f"Hello, {name}!")

greet_user("Alice")    # "Alice" is an argument
greet_user("Bob")      # "Bob" is an argument
```

### Default Parameter Value

You can define a default value for a parameter. If you call the function without an argument, it will use the default value.

```python
def greet_country(country="Norway"):
    print(f"I am from {country}")

greet_country("Sweden")  # Output: I am from Sweden
greet_country()          # Output: I am from Norway
```

### Keyword Arguments

You can also send arguments with the `key = value` syntax. This way, the order of the arguments does not matter.

```python
def display_info(name, age):
    print(f"Name: {name}, Age: {age}")

display_info(age=30, name="Alice")  # Order doesn't matter
```

---

## 3. The `return` Statement

Functions can optionally return a value. The `return` statement is used to exit a function and return a value. If no `return` statement is specified, the function returns `None`.

```python
def add_numbers(x, y):
    return x + y

result = add_numbers(5, 3)
print(result)  # Output: 8
```

A function can return multiple values. This is typically done by returning a tuple.

```python
def get_name_and_age():
    name = "Alice"
    age = 30
    return name, age

# The returned values can be unpacked into variables
user_name, user_age = get_name_and_age()

print(user_name)  # Output: Alice
print(user_age)   # Output: 30
```

---

## 4. Arbitrary Arguments: `*args` and `**kwargs`

Sometimes, you might not know in advance how many arguments will be passed into your function. Python allows you to handle this kind of situation through arbitrary arguments.

### `*args` (Non-Keyword Arguments)

If you use `*args` as a parameter, the function will receive a **tuple** of arguments, and can access the items accordingly.

```python
def sum_all(*numbers):
    total = 0
    for num in numbers:
        total += num
    return total

print(sum_all(1, 2, 3))        # Output: 6
print(sum_all(10, 20, 30, 40)) # Output: 100
```

### `**kwargs` (Keyword Arguments)

If you use `**kwargs` as a parameter, the function will receive a **dictionary** of keyword arguments.

```python
def display_user_profile(**user_info):
    for key, value in user_info.items():
        print(f"{key}: {value}")

display_user_profile(name="Alice", age=30, city="New York")
```
**Output:**
```
name: Alice
age: 30
city: New York
```

You can combine these with regular arguments, but they must be in the correct order: `standard arguments`, `*args`, `**kwargs`.

```python
def master_function(arg1, *args, **kwargs):
    print(f"Standard argument: {arg1}")
    print(f"Tuple of args: {args}")
    print(f"Dictionary of kwargs: {kwargs}")

master_function("First", "a", "b", key1="value1", key2="value2")
```

---

## 5. Docstrings

A docstring is a string literal that occurs as the first statement in a module, function, class, or method definition. It is used to document what the code does. It's a good practice to include docstrings in your functions.

```python
def calculate_area(length, width):
    """
    Calculate the area of a rectangle.

    Args:
        length (int or float): The length of the rectangle.
        width (int or float): The width of the rectangle.

    Returns:
        int or float: The calculated area of the rectangle.
    """
    return length * width

# You can access the docstring using the __doc__ attribute
print(calculate_area.__doc__)
```
