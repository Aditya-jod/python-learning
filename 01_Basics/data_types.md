# Python Data Types

In Python, every value has a data type. Data types are classifications that specify which type of value a variable can hold and what kind of mathematical, relational, or logical operations can be applied to it without causing an error.

Python has several built-in data types. Here are the most common ones:

---

## 1. Text Type: `str`

A string (`str`) is a sequence of characters, enclosed in single quotes (`'...'`), double quotes (`"..."`), or triple quotes (`"""..."""` or `'''...'''`).

```python
# Single quotes
single_quote_str = 'Hello, World!'

# Double quotes
double_quote_str = "Python is fun."

# Triple quotes for multi-line strings
multi_line_str = """This is a string
that spans across
multiple lines."""

print(single_quote_str)
print(double_quote_str)
print(multi_line_str)
```

Strings are **immutable**, which means once a string is created, it cannot be changed.

---

## 2. Numeric Types: `int`, `float`, `complex`

These types represent numbers.

-   **`int` (Integer)**: A whole number, positive or negative, without decimals.
    ```python
    my_integer = 123
    negative_integer = -45
    ```

-   **`float` (Floating-Point Number)**: A number, positive or negative, containing one or more decimals.
    ```python
    my_float = 3.14159
    negative_float = -0.001
    ```

-   **`complex` (Complex Number)**: Numbers with a real and an imaginary part, written with a "j" as the imaginary part.
    ```python
    my_complex = 2 + 3j
    ```

---

## 3. Sequence Types: `list`, `tuple`, `range`

These types store collections of items.

-   **`list`**: A collection which is **ordered** and **mutable** (changeable). Lists are written with square brackets `[]`.
    ```python
    my_list = ["apple", "banana", "cherry"]
    my_list[1] = "blueberry"  # This is allowed
    print(my_list)  # Output: ['apple', 'blueberry', 'cherry']
    ```

-   **`tuple`**: A collection which is **ordered** and **immutable** (unchangeable). Tuples are written with round brackets `()`.
    ```python
    my_tuple = ("apple", "banana", "cherry")
    # my_tuple[1] = "blueberry"  # This would cause an error
    print(my_tuple)  # Output: ('apple', 'banana', 'cherry')
    ```

-   **`range`**: Represents an immutable sequence of numbers and is commonly used for looping a specific number of times.
    ```python
    for i in range(5):  # Generates numbers from 0 to 4
        print(i)
    ```

---

## 4. Mapping Type: `dict`

-   **`dict` (Dictionary)**: A collection which is **ordered** (in Python 3.7+) and **mutable**. It stores data in `key: value` pairs. Dictionaries are written with curly brackets `{}`.
    ```python
    my_dict = {
        "name": "Alice",
        "age": 30,
        "city": "New York"
    }
    print(my_dict["name"])  # Access value by key -> Output: Alice
    my_dict["age"] = 31     # Change a value
    print(my_dict)          # Output: {'name': 'Alice', 'age': 31, 'city': 'New York'}
    ```

---

## 5. Set Types: `set`, `frozenset`

-   **`set`**: A collection which is **unordered**, **unindexed**, and **mutable**. It does not allow duplicate members. Sets are written with curly brackets `{}`.
    ```python
    my_set = {"apple", "banana", "cherry", "apple"}
    print(my_set)  # Output: {'cherry', 'apple', 'banana'} (order may vary, duplicates removed)
    ```

-   **`frozenset`**: An immutable version of a set.
    ```python
    my_frozen_set = frozenset({"apple", "banana", "cherry"})
    # my_frozen_set.add("orange") # This would cause an error
    ```

---

## 6. Boolean Type: `bool`

-   **`bool` (Boolean)**: Represents one of two values: `True` or `False`. Booleans are often the result of comparison operations.
    ```python
    is_active = True
    is_greater = 10 > 5  # This evaluates to True

    print(is_active)
    print(is_greater)
    ```

---

## 7. Binary Types: `bytes`, `bytearray`, `memoryview`

These types are used to handle binary data (raw bytes). They are more advanced and typically used in networking, file handling, or when interfacing with low-level libraries.

---

## Finding the Data Type

You can get the data type of any object by using the `type()` function.

```python
x = 5
y = "Hello"
z = [1, 2, 3]

print(type(x))  # Output: <class 'int'>
print(type(y))  # Output: <class 'str'>
print(type(z))  # Output: <class 'list'>
```
