## pandas basics

pandas is a high-level library for data manipulation and analysis built on top of NumPy. Its primary data structures are:

- Series — a 1-D labeled array (like a column)
- DataFrame — a 2-D labeled tabular structure with rows and columns (like a spreadsheet or SQL table)

This guide introduces the essentials: creating Series/DataFrame, indexing/selecting, aggregation, groupby, joins, time series handling, IO, and common tips.

### Quick setup

Install pandas (and NumPy if needed):

```powershell
python -m pip install --upgrade pip; python -m pip install pandas
```

Import pandas with the conventional alias:

```python
import pandas as pd
```

### Series — 1D labeled array

Create a Series from a list or dict:

```python
pd.Series([10, 20, 30])
pd.Series({'a': 1, 'b': 2})
```

Series have an index (labels) and dtype. You can access values with `.values` or `.to_numpy()`.

### DataFrame — 2D labelled data

Create from dict of equal-length lists, NumPy arrays, or a list of dicts:

```python
df = pd.DataFrame({'name': ['Alice', 'Bob'], 'age': [25, 30]})
```

Inspecting data:

- `df.head()` / `df.tail()` — preview
- `df.info()` — dtypes and non-null counts
- `df.describe()` — summary statistics for numeric columns
- `df.shape` — (rows, cols)

### Selecting columns and rows

Columns:

```python
df['age']        # Series
df[['name','age']]  # DataFrame with two columns
```

Rows by label/index: `df.loc[label]` or `df.loc[rows, cols]`

Rows by integer position: `df.iloc[pos]` or `df.iloc[row_slice, col_slice]`

Boolean selection:

```python
df[df['age'] > 26]
```

Setting values with `.loc` and `.iloc` is recommended to avoid SettingWithCopyWarning.

### Adding / dropping columns

```python
df['salary'] = [50000, 60000]
df = df.drop(columns=['salary'])
```

### Missing data

- `df.isna()` / `df.isnull()` — detect missing
- `df.dropna()` — drop rows/columns with missing values
- `df.fillna(value)` — replace missing values

Example:

```python
df = pd.DataFrame({'a': [1, None, 3], 'b': [4, 5, None]})
df.fillna(0)
```

### GroupBy — split, apply, combine

`groupby` followed by an aggregation or transformation is one of pandas' most powerful tools.

```python
df = pd.DataFrame({'team': ['A','A','B'], 'points':[10, 15, 7]})
df.groupby('team')['points'].sum()
```

You can chain `.agg` with multiple aggregations and rename outputs.

### Merging / joining

`pd.merge(left, right, on='key', how='inner|left|right|outer')` works like SQL joins. `df.join()` is a convenience method.

```python
a = pd.DataFrame({'id':[1,2], 'val':[10,20]})
b = pd.DataFrame({'id':[2,3], 'val2':[30,40]})
pd.merge(a, b, on='id', how='outer')
```

### Concatenation

Use `pd.concat([df1, df2], axis=0)` to stack data vertically, or axis=1 to join side-by-side.

### Time series

pandas has rich time-series support. Parse dates when reading or use `pd.to_datetime`.

```python
ts = pd.date_range('2020-01-01', periods=3, freq='D')
df = pd.DataFrame({'value':[1,2,3]}, index=ts)
df.resample('M').sum()
```

### IO — reading and writing data

- `pd.read_csv`, `df.to_csv`
- `pd.read_excel`, `df.to_excel` (requires openpyxl/xlrd)
- `pd.read_json`, `df.to_json`
- `pd.read_parquet`, `df.to_parquet` (requires pyarrow or fastparquet)

Example:

```python
df = pd.read_csv('data.csv')
df.to_parquet('data.parquet')
```

### Performance tips

- Use appropriate dtypes (e.g., `category` for string-like columns with few unique values).
- Vectorize operations; avoid `apply` with Python functions on rows (use built-in pandas methods or NumPy ufuncs).
- For large datasets, consider chunked reading (`pd.read_csv(..., chunksize=...)`) or using Dask/Polars.

### Common pitfalls

- SettingWithCopyWarning: use `.loc` to set values safely.
- Datetime parsing: specify `parse_dates` in `read_csv` to avoid surprises.
- Inplace operations: many pandas methods accept `inplace=True` but returning and assigning is often safer and clearer.

### Small examples

- Basic transformations:

```python
df = pd.DataFrame({'name':['A','B','C'],'score':[10,15,7]})
df['pass'] = df['score'] > 8
```

- Groupby + aggregation:

```python
df = pd.DataFrame({'city':['X','X','Y'], 'sales':[100,150,200]})
df.groupby('city').agg(total_sales=('sales','sum'), avg_sales=('sales','mean'))
```

- Merge and compute:

```python
left = pd.DataFrame({'id':[1,2], 'x':[10,20]})
right = pd.DataFrame({'id':[1,2], 'y':[1,2]})
res = pd.merge(left, right, on='id')
res['z'] = res['x'] * res['y']
```

### Try it (PowerShell)

Create `test_pandas.py` with a quick example and run it:

```powershell
cat > test_pandas.py <<'PY'
import pandas as pd
from io import StringIO

csv = 'name,age\nAlice,25\nBob,30\nCharlie,22'
df = pd.read_csv(StringIO(csv))
print(df)
print('mean age:', df['age'].mean())
PY

python .\test_pandas.py
```

If heredoc isn't supported, create the file with an editor or use `Set-Content`.

### Further reading

- pandas docs: https://pandas.pydata.org/docs/
- Cookbooks and tutorials: pandas user guide, official examples

### Summary

pandas provides high-level tools to load, clean, transform, aggregate, and analyze tabular data quickly. Master DataFrame creation, indexing (`.loc`, `.iloc`), `groupby`, joins, and the IO utilities to be productive.
