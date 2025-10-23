# Conditionals (if / elif / else)

Conditionals let your program make decisions. In Python, the keywords are `if`, `elif`, and `else`.

## Basic syntax

```python
x = 10
if x > 0:
    print("positive")
elif x == 0:
    print("zero")
else:
    print("negative")
```

- The colon `:` and the indented block are required.
- `elif` is shorthand for "else if" — you can have as many `elif` clauses as you need.

## Truthiness

Python evaluates many values as `False` in boolean contexts:

- `None`, `False`
- Zero of any numeric type: `0`, `0.0`
- Empty sequences/collections: `""`, `[]`, `()`, `{}`

All other values are truthy.

```python
if []:
    print("This won't run")
else:
    print("Empty list is falsy")
```

## Short-circuiting with `and` / `or`

`and` and `or` don't evaluate the second operand if the result can be determined from the first (this is called short-circuit evaluation).

```python
def expensive_check():
    print('running expensive check')
    return True

x = 0
if x != 0 and expensive_check():
    print('both true')
else:
    print('short-circuited, expensive_check() not run for x=0')
```

`or` will return the first truthy operand; `and` returns the first falsy operand or the last operand if all are truthy.

```python
# Useful trick: provide default values
name = input_value or 'Guest'
```

## Ternary conditional expression

A compact way to write simple conditionals:

```python
status = 'even' if x % 2 == 0 else 'odd'
```

## Chained comparisons

Python supports chained comparisons which read like math:

```python
if 0 < x < 10:
    print('x is between 0 and 10')
```

This is equivalent to `0 < x and x < 10` but more concise and readable.

## Common patterns and best practices

- Prefer explicit comparisons to avoid surprises with truthy/falsy values.
- Keep blocks small and focused; if a condition becomes complex, consider naming parts with variables (it improves readability).

```python
is_valid_user = (user is not None) and user.is_active
if is_valid_user:
    do_something()
```

## Examples

1. Check divisibility:

```python
n = 15
if n % 3 == 0 and n % 5 == 0:
    print('fizzbuzz')
elif n % 3 == 0:
    print('fizz')
elif n % 5 == 0:
    print('buzz')
else:
    print(n)
```

2. Grading example:

```python
score = 78
if score >= 90:
    grade = 'A'
elif score >= 80:
    grade = 'B'
elif score >= 70:
    grade = 'C'
elif score >= 60:
    grade = 'D'
else:
    grade = 'F'
print(grade)
```

## Exercises

1. Write a function `sign(x)` that returns `1` if `x>0`, `0` if `x==0`, and `-1` if `x<0`.
2. Write `is_leap_year(year)` that returns `True` if `year` is a leap year (divisible by 4 but not by 100, unless divisible by 400).
3. Given three numbers `a`, `b`, `c`, print them in ascending order using conditionals only (no sorting functions).

---

If you want, I can add solutions in a separate `01_Basics/solutions/conditionals_solutions.md` or keep them in a `solutions/` folder. Let me know your preference.