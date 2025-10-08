# List Comprehensions in Python

List comprehensions provide a concise and readable way to create lists. They are often more efficient and easier to understand than using a `for` loop to build a list.

---

## 1. Basic Syntax

The basic syntax of a list comprehension is:

`[expression for item in iterable]`

This is equivalent to the following `for` loop:

```python
new_list = []
for item in iterable:
    new_list.append(expression)
```

### Example: Squaring Numbers

Let's create a list of the first 5 square numbers.

**Using a `for` loop:**
```python
squares = []
for i in range(1, 6):
    squares.append(i * i)

print(squares)  # Output: [1, 4, 9, 16, 25]
```

**Using a list comprehension:**
```python
squares = [i * i for i in range(1, 6)]

print(squares)  # Output: [1, 4, 9, 16, 25]
```
As you can see, the list comprehension is much shorter and more direct.

---

## 2. Adding a Conditional `if` Statement

You can add a condition to filter the items from the iterable.

The syntax is:

`[expression for item in iterable if condition]`

### Example: Getting Even Numbers

Let's create a list of even numbers from 0 to 9.

**Using a `for` loop:**
```python
evens = []
for i in range(10):
    if i % 2 == 0:
        evens.append(i)

print(evens)  # Output: [0, 2, 4, 6, 8]
```

**Using a list comprehension:**
```python
evens = [i for i in range(10) if i % 2 == 0]

print(evens)  # Output: [0, 2, 4, 6, 8]
```

---

## 3. Using `if-else` in a List Comprehension

You can also use an `if-else` statement to change the expression based on a condition. Note that the syntax is different from a simple `if` filter.

The syntax is:

`[expression_if_true if condition else expression_if_false for item in iterable]`

The `if-else` block comes **before** the `for` loop.

### Example: Categorizing Numbers

Let's create a list that labels numbers as "Even" or "Odd".

**Using a `for` loop:**
```python
labels = []
for i in range(10):
    if i % 2 == 0:
        labels.append("Even")
    else:
        labels.append("Odd")

print(labels)
# Output: ['Even', 'Odd', 'Even', 'Odd', 'Even', 'Odd', 'Even', 'Odd', 'Even', 'Odd']
```

**Using a list comprehension:**
```python
labels = ["Even" if i % 2 == 0 else "Odd" for i in range(10)]

print(labels)
# Output: ['Even', 'Odd', 'Even', 'Odd', 'Even', 'Odd', 'Even', 'Odd', 'Even', 'Odd']
```

---

## 4. Nested List Comprehensions

You can use nested loops within a list comprehension to work with nested lists (like matrices).

### Example: Flattening a Matrix

Let's convert a 2D list (a list of lists) into a single 1D list.

```python
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

# Using a nested for loop
flattened = []
for row in matrix:
    for num in row:
        flattened.append(num)

print(flattened)  # Output: [1, 2, 3, 4, 5, 6, 7, 8, 9]

# Using a nested list comprehension
flattened_comp = [num for row in matrix for num in row]

print(flattened_comp)  # Output: [1, 2, 3, 4, 5, 6, 7, 8, 9]
```
The order of the `for` clauses is the same as in the nested loop.

---

## Why Use List Comprehensions?

1.  **Conciseness and Readability**: They allow you to write complex list creation logic in a single, readable line.
2.  **Performance**: They are often faster than creating the same list using a `for` loop because the looping logic is implemented in C, which is faster than Python's `for` loop interpretation.
3.  **Pythonic**: Using list comprehensions is considered a more "Pythonic" way of writing code, which means it follows the common conventions and idioms of the Python language.
