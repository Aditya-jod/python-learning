# Decorators in Python

A decorator is a design pattern in Python that allows a user to add new functionality to an existing object (like a function or a class) without modifying its structure. Decorators are a powerful and elegant way to wrap code around functions.

They are typically expressed with the `@decorator_name` syntax placed on the line before the function definition.

---

## 1. Understanding Functions as First-Class Objects

Before diving into decorators, it's crucial to understand that in Python, functions are "first-class objects." This means that functions can be:
-   Assigned to a variable.
-   Passed as an argument to another function.
-   Returned from another function.

```python
def greet(name):
    return f"Hello, {name}!"

# 1. Assign a function to a variable
say_hello = greet
print(say_hello("Alice"))  # Output: Hello, Alice!

# 2. Pass a function as an argument
def process_greeting(greeter_func, name):
    return greeter_func(name).upper()

print(process_greeting(greet, "Bob")) # Output: HELLO, BOB!
```

---

## 2. A Simple Decorator

A decorator is essentially a function that takes another function as an argument, adds some functionality, and then returns another function.

Let's create a simple decorator that logs when a function is executed.

```python
# This is the decorator function
def my_logger(original_function):
    
    # The 'wrapper' function is what gets executed
    def wrapper(*args, **kwargs):
        print(f"Executing {original_function.__name__}...")
        result = original_function(*args, **kwargs) # Call the original function
        print(f"Finished executing {original_function.__name__}.")
        return result
        
    return wrapper

# Now, let's apply this decorator to a function
@my_logger
def display_info(name, age):
    print(f"display_info ran with arguments ({name}, {age})")

# Call the decorated function
display_info("Alice", 30)
```

**Output:**
```
Executing display_info...
display_info ran with arguments (Alice, 30)
Finished executing display_info.
```

### What `@my_logger` Does

The `@my_logger` syntax is just "syntactic sugar" for the following:

```python
def display_info(name, age):
    print(f"display_info ran with arguments ({name}, {age})")

# Manually decorate the function
decorated_display_info = my_logger(display_info)

# Call the returned wrapper function
decorated_display_info("Alice", 30)
```
The `@` symbol makes this process much cleaner and more readable.

**Note on `*args` and `**kwargs`**: The `wrapper` function uses `*args` and `**kwargs` to ensure that it can accept any number of positional and keyword arguments, making the decorator versatile enough to be used on any function.

---

## 3. Preserving Function Metadata

When you decorate a function, you are technically replacing it with the wrapper function. This means the original function's metadata (like its name `__name__` and its docstring `__doc__`) is lost.

```python
@my_logger
def say_hello():
    """A simple function to say hello."""
    print("Hello!")

print(say_hello.__name__)  # Output: wrapper (not 'say_hello')
print(say_hello.__doc__)   # Output: None
```

To fix this, Python provides a helper decorator called `functools.wraps`. You use it to decorate your `wrapper` function inside the decorator.

```python
import functools

def my_logger_fixed(original_function):
    
    @functools.wraps(original_function) # This is the fix
    def wrapper(*args, **kwargs):
        print(f"Executing {original_function.__name__}...")
        result = original_function(*args, **kwargs)
        print(f"Finished executing {original_function.__name__}.")
        return result
        
    return wrapper

@my_logger_fixed
def say_hello_fixed():
    """A simple function to say hello."""
    print("Hello!")

print(say_hello_fixed.__name__)  # Output: say_hello_fixed
print(say_hello_fixed.__doc__)   # Output: A simple function to say hello.
```

---

## 4. Decorators with Arguments

Sometimes, you might want to pass arguments to your decorator itself. To do this, you need to add another layer of function nesting.

Let's create a decorator that repeats a function's execution a specified number of times.

```python
def repeat(num_times):
    # This outer function takes the decorator's argument
    def decorator_repeat(func):
        # This is the actual decorator
        @functools.wraps(func)
        def wrapper(*args, **kwargs):
            # This is the wrapper that gets executed
            for _ in range(num_times):
                result = func(*args, **kwargs)
            return result
        return wrapper
    return decorator_repeat

# Now use the decorator with an argument
@repeat(num_times=3)
def greet(name):
    print(f"Hello, {name}!")

greet("Alice")
```
**Output:**
```
Hello, Alice!
Hello, Alice!
Hello, Alice!
```

### Common Use Cases for Decorators

-   **Logging**: To log function calls, arguments, and return values.
-   **Timing**: To measure the execution time of a function.
-   **Authentication/Authorization**: In web frameworks (like Flask or Django), decorators are used to check if a user is logged in before allowing them to access a specific page.
-   **Caching**: To store the results of expensive function calls and return the cached result when the same inputs occur again.
