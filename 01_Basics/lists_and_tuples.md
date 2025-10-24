# Lists and Tuples

Lists and tuples are the basic sequence types in Python. They look similar at first glance but have different use cases and behaviors. I’ll walk you through practical examples and tips I wish someone had shown me when I was starting.

---

## 1. Creating lists and tuples

Lists use square brackets and are mutable (you can change them):

```python
fruits = ['apple', 'banana', 'cherry']
numbers = [1, 2, 3, 4]
mixed = ['text', 10, 3.14, True]
```

Tuples use parentheses (or no punctuation for simple literals) and are immutable:

```python
point = (10, 20)
coords = 1, 2, 3   # also a tuple
single = (5,)      # note the trailing comma for a single-element tuple
```

Why choose one over the other? Use a list when you expect to modify the collection (append/pop/sort). Use a tuple when the data should not change (safety, hashability — tuples can be dictionary keys if they contain only hashable items).

---

## 2. Accessing items: indexing and slicing

Both lists and tuples support indexing and slicing:

```python
items = ['a', 'b', 'c', 'd']
items[0]    # 'a'
items[-1]   # 'd'
items[1:3]  # ['b', 'c']
```

Slicing returns the same sequence type (`list` slices give lists).

---

## 3. Common list methods (mutating operations)

- `append(x)` — add `x` to end
- `extend(iterable)` — extend by elements from iterable
- `insert(i, x)` — insert `x` at index `i`
- `remove(x)` — remove first occurrence of `x` (ValueError if not found)
- `pop([i])` — remove and return item at `i` (default last)
- `clear()` — remove all items
- `sort()` — sort in-place
- `reverse()` — reverse in-place

Example:

```python
nums = [3, 1, 4]
nums.append(2)      # [3, 1, 4, 2]
nums.sort()         # [1, 2, 3, 4]
val = nums.pop()    # val=4, nums=[1,2,3]
```

If you want a new sorted list without changing the original, use `sorted()` which returns a new list.

---

## 4. Tuple behavior and use-cases

Tuples are immutable — once created, you cannot change their contents.

```python
t = (1, 2, 3)
# t[0] = 5  # TypeError
```

Tuples are useful when:
- You want a lightweight record (e.g., `(x, y)`) or fixed collection.
- You need a hashable sequence (e.g., use a tuple as a dictionary key).
- You want to signal “this collection shouldn't change" to other programmers.

A common Python idiom: returning multiple values from a function using a tuple:

```python
def min_max(values):
    return min(values), max(values)

lo, hi = min_max([3, 7, 1])
```

---

## 5. Mutability pitfalls

A list inside a tuple remains mutable, because immutability applies to the container, not the contained objects:

```python
t = ([1,2], 3)
t[0].append(4)   # allowed — t now is ([1,2,4], 3)
```

If you need to prevent any change, avoid nesting mutable objects or use deep copies and careful design.

---

## 6. Iteration patterns and unpacking

You can iterate over lists and tuples with `for` loops, and unpack values directly:

```python
pairs = [(1,2), (3,4), (5,6)]
for a, b in pairs:
    print(a + b)

# swapping values
x, y = 1, 2
x, y = y, x
```

Unpacking is also handy with the star operator:

```python
first, *middle, last = [1, 2, 3, 4, 5]
```

---

## 7. List comprehensions (concise and fast)

List comprehensions are a very Pythonic way to create lists from iterables.

```python
squares = [x*x for x in range(10)]
evens = [x for x in range(20) if x % 2 == 0]
```

They are usually faster and clearer than building lists with loops.

---

## 8. Converting between types

```python
lst = list((1,2,3))   # from tuple to list
tpl = tuple([1,2,3])  # from list to tuple
```

Also, `list('abc')` yields `['a','b','c']` and `''.join(list_of_strings)` joins strings into one.

---

## 9. Performance notes

- Lists are dynamic arrays; indexing is O(1), inserting/removing at the end is amortized O(1), but inserting/removing in the middle is O(n).
- Tuples are slightly more memory efficient and can be marginally faster to iterate.

In most beginner projects the difference is negligible; choose based on semantics (mutable vs immutable) first.

---

## 10. Examples

- Flatten a list of lists:

```python
matrix = [[1,2], [3,4], [5,6]]
flat = [x for row in matrix for x in row]
```

- Use a tuple as a dict key:

```python
visits = {}
point = (10, 20)
visits[point] = visits.get(point, 0) + 1
```

---

## Exercises

1. Write `unique_preserve_order(lst)` which returns a list of unique items preserving the original order.
2. Given a list of integers, return a list of tuples `(x, x*x)` for each even `x` using a list comprehension.
3. Implement `chunk_list(lst, n)` which splits `lst` into chunks of size `n`.
4. Explain (in a sentence) when you'd pick a tuple over a list.

---

If you want, I can add a `solutions/` directory and put solutions there so learners can try first.