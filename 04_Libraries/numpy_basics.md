## NumPy basics

NumPy (Numerical Python) is the fundamental package for scientific computing with Python. It provides the ndarray — a fast, efficient multidimensional array object — along with functions for performing elementwise operations, linear algebra, random sampling, and more.

This guide covers the essentials you need to start using NumPy: creating arrays, inspecting them, indexing, broadcasting, common operations, linear algebra, random numbers, IO, and tips for performance and debugging.

### Quick setup

Install NumPy if you don't already have it:

```powershell
python -m pip install --upgrade pip; python -m pip install numpy
```

In a Python script or REPL, import NumPy with the conventional alias:

```python
import numpy as np
```

### Array (ndarray) — the core object

An ndarray is a fixed-size, homogeneous n-dimensional array. Key attributes:

- `ndarray.ndim`: number of dimensions (axes)
- `ndarray.shape`: tuple giving the size in each dimension
- `ndarray.size`: total number of elements
- `ndarray.dtype`: data type of elements (e.g., `float64`, `int32`)
- `ndarray.itemsize`: bytes per element

Example:

```python
import numpy as np

a = np.array([1, 2, 3])        # 1D array
M = np.array([[1, 2], [3, 4]]) # 2D array (matrix)
print(a.shape, a.dtype)        # (3,) int64 (dtype depends on platform)
print(M.shape)                 # (2, 2)
```

### Creating arrays

Basic factories:
- `np.array` — create from Python lists
- `np.zeros`, `np.ones`, `np.empty` — initialize with values
- `np.arange`, `np.linspace` — ranges
- `np.eye` — identity matrix
- `np.full` — fill with a constant
- `np.random.*` — random arrays (see below)

Examples:

```python
np.zeros((2,3))        # 2x3 array of zeros
np.ones(4)             # 1D array of ones
np.empty((3,))         # uninitialized array (fast)
np.arange(0, 10, 2)    # [0,2,4,6,8]
np.linspace(0, 1, 5)   # [0., 0.25, 0.5, 0.75, 1.]
np.eye(3)              # 3x3 identity matrix
np.full((2,2), 7)      # 2x2 array filled with 7
```

### Data types (dtype)

NumPy arrays have a single dtype. Common types: `int8/16/32/64`, `float16/32/64`, `bool`, `complex64/128`.

Specify dtype when creating arrays:

```python
np.array([1, 2, 3], dtype=np.float32)
```

Converting between types: `astype` (creates a copy)

```python
arr = np.array([1.2, 3.4])
arr_int = arr.astype(np.int64)  # [1, 3]
```

### Indexing and slicing

Indexing works similarly to lists but with more axes.

```python
x = np.arange(12).reshape(3,4)
# x = [[ 0, 1, 2, 3],
#      [ 4, 5, 6, 7],
#      [ 8, 9,10,11]]
x[0, 1]    # 1
x[1]       # row [4,5,6,7]
x[:, 2]    # column [2,6,10]
x[0:2, 1:3]# slice -> shape (2,2)
```

Boolean (mask) indexing and fancy (integer) indexing:

```python
mask = x % 2 == 0
x[mask]         # all even elements as 1D array
cols = [0, 2]
x[:, cols]      # select columns 0 and 2
```

Note: fancy indexing always returns a copy; slicing returns a view (no copy) where possible.

### Broadcasting — working with different shapes

Broadcasting lets you perform arithmetic between arrays of different shapes when their dimensions are compatible.

Rules (short):
1. If arrays have different ndim, prepend 1s to the smaller shape.
2. For each axis, the sizes must match or one of them must be 1.
3. The result has the maximum size along each axis.

Examples:

```python
row = np.array([1, 2, 3])        # shape (3,)
M = np.ones((4,3)) * row         # row broadcasts to every row -> shape (4,3)
col = np.array([[0], [1], [2], [3]]) # shape (4,1)
M + col                          # adds column vector to each column
```

Broadcasting avoids explicit loops and is vectorized (fast).

### Universal functions (ufuncs)

NumPy provides vectorized functions (ufuncs) that operate elementwise: `np.sin`, `np.exp`, `np.add`, etc.

```python
arr = np.array([0, np.pi/2, np.pi])
np.sin(arr)
np.exp(arr)
np.add(arr, 1)
```

Ufuncs are fast because they run at C speed and avoid Python-level loops.

### Aggregations / reductions

Common reductions: `sum`, `mean`, `max`, `min`, `prod`, `std`, `var`.

They accept an `axis` argument to reduce along a specific axis and `keepdims=True` to preserve dimensions.

```python
M = np.arange(12).reshape(3,4)
M.sum()          # total sum
M.sum(axis=0)    # sum for each column -> shape (4,)
M.mean(axis=1)   # mean for each row -> shape (3,)
```

Use `np.argmax` / `np.argmin` to get indices of extrema.

### Linear algebra

NumPy supports basic linear algebra in `np.linalg` (matrix multiply, inverse, eigenvalues, etc.). For heavy-duty linear algebra, consider SciPy.

```python
A = np.array([[1., 2.], [3., 4.]])
b = np.array([1., 0.])
np.dot(A, b)            # matrix-vector product
A @ b                  # equivalent (Python 3.5+)
np.linalg.inv(A)       # inverse
np.linalg.solve(A, b)  # solve Ax = b (preferred to inv)
np.linalg.eig(A)       # eigenvalues and eigenvectors
```

### Random numbers

Use the `numpy.random` module. As of NumPy 1.17+, a new Generator API is recommended.

```python
from numpy.random import default_rng
rng = default_rng(42)
rng.random(5)          # 5 random floats in [0,1)
rng.integers(0, 10, size=(3,))
rng.normal(loc=0, scale=1, size=(2,3))
```

For reproducible work, set the seed via the Generator (as above).

### Input / Output (saving and loading)

- `np.save` / `np.savez` / `np.savez_compressed` for binary .npy/.npz files
- `np.load` to read .npy/.npz
- `np.savetxt` / `np.loadtxt` for text files (CSV-like). Use `delimiter=','` for CSV.

Examples:

```python
np.save('arr.npy', M)
loaded = np.load('arr.npy')
np.savetxt('arr.csv', M, delimiter=',')
```

For larger datasets or complex metadata, consider HDF5 (h5py) or Zarr.

### Performance tips

- Prefer vectorized operations (ufuncs) over Python loops.
- Use appropriate dtypes to save memory (e.g., `float32` vs `float64`).
- Beware of creating many temporary arrays; use `out=` parameter in ufuncs when possible.
- Use `np.dot` / `@` and BLAS-backed functions for linear algebra (they're fast if NumPy was built with optimized BLAS).

Example: use out parameter

```python
res = np.empty_like(M)
np.add(M, 1, out=res)
```

### Common pitfalls

- Mixed dtypes: NumPy upcasts to a common dtype which may surprise you.
- Integer division (in Python 3 using NumPy integers does true division returning floats for `/`). Use `//` for integer division.
- Slicing returns views — modifying a slice may modify the original array. Use `.copy()` to get a separate array.
- Fancy indexing returns copies — changes won't affect the original array.

```python
a = np.arange(5)
v = a[1:4]       # view
v[0] = 100       # a is modified
v2 = a[[1,2,3]]  # fancy indexing -> copy
v2[0] = -1       # a is not modified
```

### Small examples

- Compute column means for a 2D dataset:

```python
data = rng.normal(size=(100, 5))
col_means = data.mean(axis=0)
```

- Standardize data (zero mean, unit variance) column-wise:

```python
means = data.mean(axis=0)
stds = data.std(axis=0)
data_standardized = (data - means) / stds
```

- Matrix multiplication and solving linear systems:

```python
A = rng.normal(size=(3,3))
b = rng.normal(size=(3,))
x = np.linalg.solve(A, b)
```

### Try it (PowerShell)

Create a file `test_numpy.py` with a simple example and run it.

```powershell
# create file
cat > test_numpy.py <<'PY'
import numpy as np
from numpy.random import default_rng
rng = default_rng(0)
M = rng.normal(size=(4,4))
print('M:\n', M)
print('column means:', M.mean(axis=0))
PY

python .\test_numpy.py
```

(On PowerShell the `cat > file <<'PY'` heredoc works in recent versions; if it doesn't, create the file in an editor or use `Set-Content`.)

### Further reading and next steps

- Official docs: https://numpy.org/doc/stable/
- Tutorials: NumPy User Guide and NumPy Quickstart
- For data analysis, combine NumPy with pandas; for scientific computing, add SciPy.

### Summary

NumPy provides the ndarray, powerful vectorized operations, and tools for numerical work in Python. Focus on mastering array creation/reshaping, indexing, broadcasting, and ufuncs — they unlock most of NumPy's power.

