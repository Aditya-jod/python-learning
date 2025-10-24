# Dictionaries (mapping type)

Dictionaries are Python's built-in mapping type — they store key → value pairs and are super useful for structured data, counting, grouping, and lookups.

---

## 1. Creating dictionaries

```python
# literal
person = {'name': 'Alice', 'age': 25}

# from pairs
pairs = [('a', 1), ('b', 2)]
d = dict(pairs)

# empty dict
empty = {}
```

Keys must be hashable (strings, numbers, tuples of immutables). Values can be anything.

---

## 2. Accessing and setting values

```python
name = person['name']       # KeyError if missing
age = person.get('age')     # returns None if missing
age2 = person.get('age', 0) # default value

person['city'] = 'Delhi'    # add or update
```

Use `in` to check keys:

```python
if 'salary' in person:
    print(person['salary'])
```

---

## 3. Iterating dictionaries

By default, iterating a dict yields its keys:

```python
for k in person:
    print(k, person[k])

# useful forms
for k, v in person.items():
    print(k, v)

for k in person.keys():
    print(k)

for v in person.values():
    print(v)
```

---

## 4. Useful dict methods

- `d.keys()`, `d.values()`, `d.items()`
- `d.get(key, default)`
- `d.pop(key, default)` — remove and return
- `d.update(other)` — merge from another dict
- `d.clear()` — remove all items

Merging in Python 3.9+: `d3 = d1 | d2` (creates new dict)

---

## 5. Common patterns

### Counting / frequency

```python
words = ['a', 'b', 'a']
count = {}
for w in words:
    count[w] = count.get(w, 0) + 1
```

This pattern is so common that Python provides `collections.Counter` which does it neatly:

```python
from collections import Counter
Counter(words)
```

### Grouping

```python
pairs = [('Alice', 'NY'), ('Bob', 'CA'), ('Alice', 'TX')]
groups = {}
for name, state in pairs:
    groups.setdefault(name, []).append(state)
```

`defaultdict(list)` makes this even cleaner:

```python
from collections import defaultdict
groups = defaultdict(list)
for name, state in pairs:
    groups[name].append(state)
```

---

## 6. Dictionary comprehensions

Like list comprehensions, dict comprehensions are concise:

```python
squares = {x: x*x for x in range(6)}
```

They are handy for transforming one mapping to another.

---

## 7. Nested dictionaries

Sometimes values are dictionaries themselves. Access carefully and consider `get` to avoid KeyError:

```python
data = {'user': {'name': 'Alice', 'age': 25}}
name = data.get('user', {}).get('name')
```

---

## 8. Immutability and copy

Assignment `d2 = d1` makes `d2` reference the same object. Use `d1.copy()` for a shallow copy; use `copy.deepcopy()` for nested structures.

```python
import copy
d2 = copy.deepcopy(d1)
```

---

## 9. Examples

- Build an index mapping words to positions in a text:

```python
text = 'to be or not to be'
index = {}
for pos, word in enumerate(text.split()):
    index.setdefault(word, []).append(pos)
```

- Merge two dicts, preferring values from the second:

```python
a = {'x': 1, 'y': 2}
b = {'y': 9, 'z': 3}
merged = {**a, **b}  # {'x':1, 'y':9, 'z':3}
```

---

## 10. Exercises

1. `char_freq(s)`: return a dict counting each character in string `s`.
2. `invert_dict(d)`: given a dict mapping keys→values (values unique), return a new dict mapping values→keys.
3. `group_by_key(pairs)`: given a list of `(k, v)` pairs, return a dict mapping `k` to list of values.
4. Given a list of dicts with numeric field `score`, find the dict with the maximum score (hint: `max(list_of_dicts, key=lambda x: x['score'])`).

---

If you'd like, I can add brief solutions to a `01_Basics/solutions/` folder, or keep the exercises separate from the answers so learners can try first.