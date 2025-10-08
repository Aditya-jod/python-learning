# Loops in Python

Loops are a fundamental concept in programming that allow you to execute a block of code repeatedly. Python has two primary types of loops: `for` loops and `while` loops.

---

## 1. The `for` Loop

A `for` loop is used for **iterating over a sequence** (such as a list, tuple, dictionary, set, or string). This is less like the `for` keyword in other programming languages and works more like an iterator method.

### Iterating over a List

```python
fruits = ["apple", "banana", "cherry"]

for fruit in fruits:
    print(fruit)
```
**Output:**
```
apple
banana
cherry
```

### Iterating over a String

A string is a sequence of characters, so you can loop through it.

```python
for letter in "Python":
    print(letter)
```
**Output:**
```
P
y
t
h
o
n
```

### The `range()` Function

To loop through a set of code a specified number of times, we can use the `range()` function. `range()` generates a sequence of numbers.

```python
# Loop 5 times, from 0 to 4
for i in range(5):
    print(i)

# Loop from 2 to 5 (exclusive)
for i in range(2, 5):
    print(i)

# Loop from 0 to 10, with a step of 2
for i in range(0, 10, 2):
    print(i)
```

### The `break` Statement

With the `break` statement, we can stop the loop before it has looped through all the items.

```python
fruits = ["apple", "banana", "cherry"]
for fruit in fruits:
    if fruit == "banana":
        break  # Stop the loop
    print(fruit)
```
**Output:**
```
apple
```

### The `continue` Statement

With the `continue` statement, we can stop the current iteration of the loop and continue with the next.

```python
fruits = ["apple", "banana", "cherry"]
for fruit in fruits:
    if fruit == "banana":
        continue  # Skip "banana" and go to the next iteration
    print(fruit)
```
**Output:**
```
apple
cherry
```

### The `else` in `for` Loop

The `else` keyword in a `for` loop specifies a block of code to be executed when the loop is finished.

```python
for i in range(3):
    print(i)
else:
    print("Loop finished successfully!")
```
**Note:** The `else` block will **not** be executed if the loop is stopped by a `break` statement.

---

## 2. The `while` Loop

A `while` loop is used to execute a block of statements as long as a given condition is `True`.

```python
i = 1
while i < 6:
    print(i)
    i += 1  # It's crucial to increment i, otherwise the loop will continue forever
```
**Output:**
```
1
2
3
4
5
```

### The `break` Statement in `while`

You can use `break` to exit a `while` loop, just like in a `for` loop.

```python
i = 1
while i < 6:
    if i == 3:
        break
    print(i)
    i += 1
```
**Output:**
```
1
2
```

### The `continue` Statement in `while`

`continue` can be used to skip the current iteration and move to the next.

```python
i = 0
while i < 6:
    i += 1
    if i == 3:
        continue
    print(i)
```
**Output:**
```
1
2
4
5
6
```

### The `else` in `while` Loop

You can also have an `else` block with a `while` loop. The `else` block is executed when the condition becomes `False`.

```python
i = 1
while i < 4:
    print(i)
    i += 1
else:
    print("The while loop condition is now false.")
```

---

## 3. Nested Loops

You can use a loop inside another loop. This is called a nested loop.

```python
adjectives = ["red", "big", "tasty"]
fruits = ["apple", "banana", "cherry"]

for adj in adjectives:
    for fruit in fruits:
        print(adj, fruit)
```
**Output:**
```
red apple
red banana
red cherry
big apple
big banana
big cherry
tasty apple
tasty banana
tasty cherry
```
