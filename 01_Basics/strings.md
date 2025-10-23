# Strings

Strings represent text. Python's string support is rich and easy to use.

## Creating strings

```python
s1 = 'hello'
s2 = "world"
multi = """This is a
multi-line string"""
raw = r"C:\\path\\to\\file"
```

## Indexing and slicing

Strings are sequences, so you can index and slice them like lists.

```python
s = 'python'
s[0]    # 'p'
s[-1]   # 'n'
s[1:4]  # 'yth'
```

Remember slices return new strings — strings are immutable.

## Common string methods

- `s.lower()`, `s.upper()` — case conversion
- `s.strip()` — remove whitespace at both ends
- `s.split(sep)` — split into a list of substrings
- `sep.join(list_of_strings)` — join with a separator
- `s.replace(old, new)` — replace substrings
- `s.find(sub)` / `s.index(sub)` — find substring position
- `s.startswith(prefix)` / `s.endswith(suffix)`

Example:

```python
line = '  Alice, 25, Engineer\n'
name, age, job = [x.strip() for x in line.strip().split(',')]
```

## f-strings (formatted string literals)

Python 3.6+ has f-strings — concise and powerful:

```python
name = 'Alice'
age = 25
s = f'{name} is {age} years old'
```

You can include expressions:

```python
s = f'{name.upper()} will be {age+1} next year'
```

## Formatting numbers

Use format specifiers inside f-strings:

```python
pi = 3.14159
f'{pi:.2f}'   # '3.14'
f'{1000:,}'   # '1,000'
```

## Encoding and Bytes

For most learning tasks you can stick with `str`. When working with files or network APIs you may see `bytes`.

```python
b = 'hello'.encode('utf-8')
'some bytes'.encode()
'some bytes'.encode().decode('utf-8')
```

## Useful patterns

- Normalizing text:

```python
s = "  Hello World \n"
s_norm = s.strip().lower()
```

- Safe substring extraction:

```python
s = 'abc'
sub = s[:10]  # no IndexError, returns 'abc'
```

- Splitting CSV-like lines:

```python
row = 'a, b, c'
fields = [f.strip() for f in row.split(',')]
```

## Exercises

1. `normalize_name(s)`: accept a string like `'  aLIcE  '` and return `'Alice'`.
2. `extract_domain(email)`: given `'user@example.com'` return `'example.com'`.
3. `is_palindrome(s)`: return True if the string is a palindrome (ignore spaces and case), e.g., `'A man a plan a canal Panama'`.
4. `format_currency(n)`: return a string like `'$1,234.56'` for the number `1234.56`.

---

Want solutions added? I can create `01_Basics/solutions/strings_solutions.md` or include them inline under each exercise. Also, tell me if you'd like additional examples (regex basics, transliteration, Unicode notes).