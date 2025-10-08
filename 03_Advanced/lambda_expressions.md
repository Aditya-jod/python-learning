# Lambda Expressions in Python

A lambda expression (or lambda function) is a small, anonymous function defined with the `lambda` keyword. They are like normal functions but are defined without a name.

Lambdas are restricted to a single expression and are often used for short, simple operations where a full function definition would be overly verbose.

---

## 1. Syntax

The syntax of a lambda function is straightforward:

```python
lambda arguments: expression
```

-   `lambda`: The keyword that introduces the anonymous function.
-   `arguments`: One or more arguments, separated by commas (just like a regular function).
-   `expression`: A single expression that is evaluated and returned.

### Example: A Simple Lambda

Let's compare a regular function with a lambda function that adds two numbers.

**Regular Function (`def`):**
```python
def add(x, y):
    return x + y
```

**Lambda Function:**
```python
lambda x, y: x + y
```

The lambda function is functionally identical to the `add` function but has no name.

---

## 2. How to Use Lambda Functions

You can assign a lambda to a variable, but this is generally discouraged because it offers little benefit over a `def` function (which has a proper name for debugging).

```python
# You can do this, but it's not the primary use case
adder = lambda x, y: x + y
print(adder(5, 3)) # Output: 8
```

The **real power** of lambda functions comes from using them as arguments to **higher-order functions** (functions that take other functions as input). Common examples include `sorted()`, `map()`, and `filter()`.

---

## 3. Use Case 1: Sorting with `sorted()`

The `sorted()` function can take a `key` argument, which is a function that tells `sorted()` how to determine the sorting order. Lambdas are perfect for this.

### Example: Sorting a List of Tuples

Imagine you have a list of `(item, price)` tuples and you want to sort them by price.

```python
products = [('Laptop', 999), ('Mouse', 25), ('Keyboard', 75)]

# Sort by the second element (index 1) of each tuple
sorted_by_price = sorted(products, key=lambda item: item[1])

print(sorted_by_price)
# Output: [('Mouse', 25), ('Keyboard', 75), ('Laptop', 999)]
```
Without a lambda, you would have to define a separate function just for this simple key extraction.

---

## 4. Use Case 2: Transforming with `map()`

The `map()` function applies a given function to every item of an iterable (like a list) and returns a map object (which can be converted to a list).

### Example: Squaring Numbers

```python
numbers = [1, 2, 3, 4, 5]

# Use a lambda to square each number
squared_numbers = map(lambda x: x * x, numbers)

print(list(squared_numbers))
# Output: [1, 4, 9, 16, 25]
```

---

## 5. Use Case 3: Filtering with `filter()`

The `filter()` function constructs an iterator from elements of an iterable for which a function returns `True`.

### Example: Filtering Even Numbers

```python
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

# Use a lambda to check for even numbers
even_numbers = filter(lambda x: x % 2 == 0, numbers)

print(list(even_numbers))
# Output: [2, 4, 6, 8, 10]
```

---

## 6. Limitations and Best Practices

1.  **Single Expression Only**: A lambda can only contain one expression. You cannot include statements like `if`, `for`, `while`, or `return` (the expression's result is implicitly returned).
    -   You *can* use a conditional (ternary) expression: `lambda x: 'Even' if x % 2 == 0 else 'Odd'`

2.  **Keep It Simple**: The main advantage of a lambda is its conciseness. If your logic is complex or requires multiple lines, **use a regular `def` function**. Code readability is more important than avoiding one extra line of code.

3.  **Avoid Assigning to Variables**: As mentioned earlier, `adder = lambda x, y: x + y` is less readable and provides poorer debugging information than `def adder(x, y): return x + y`. The primary use of lambdas is for situations where you don't need to name the function at all.

In summary, lambda functions are a powerful tool for writing clean, functional-style code in Python, especially when working with higher-order functions.
