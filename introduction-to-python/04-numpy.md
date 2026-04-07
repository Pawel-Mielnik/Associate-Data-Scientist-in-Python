

# NumPy Arrays and Basic Statistics

## 1. Why plain Python lists are not enough

Regular Python lists are very flexible, but they have a critical limitation for data analysis:

- they **do not support vectorised, element‑wise math** out of the box.

Example – trying to compute BMI for several people:

```python
weights = [68.7, 75.2, 80.1]
heights = [1.75, 1.82, 1.90]

# this will NOT work:
bmi = weights / heights      # TypeError
```

Python does not know how to divide one list by another.
For numerical work we need a dedicated structure – this is what **NumPy** provides.

---

## 2. NumPy arrays – the core idea

**NumPy** introduces its own array type (`numpy.ndarray`):

- behaves a bit like a list,
- all elements have the **same data type**,
- supports fast, element‑wise operations and vectorised math.


### 2.1. Creating NumPy arrays

Typical import convention:

```python
import numpy as np
```

Converting Python lists to arrays:

```python
np_heights = np.array(heights)
np_weights = np.array(weights)
```


### 2.2. Element‑wise computations

Now vectorised code works:

```python
bmi = np_weights / np_heights ** 2
```

This means:

- first element of `np_weights` divided by squared first element of `np_heights`,
- second by second, and so on.

---

## 3. One data type per array

Unlike Python lists, a NumPy array must be **homogeneous**:

- all values share the same data type (all `float`, all `int`, all `bool`, etc.).

If you mix types in the input list, NumPy will up‑cast everything to a single, more general type (often `float` or `str`) so that the array stays consistent.

---

## 4. Operators: lists vs NumPy arrays

The same operator may behave differently:

- **Lists**:
    - `a + b` → concatenation (append elements of `b` after elements of `a`).
- **NumPy arrays**:
    - `a + b` → element‑wise addition.

Example:

```python
a_list = 
b_list = 
print(a_list + b_list)        # 

a_np = np.array()
b_np = np.array()
print(a_np + b_np)            # 
```

This “math on whole arrays” behaviour is one of the main reasons NumPy is so powerful in data science.

---

## 5. Boolean indexing (logical subsetting)

NumPy has a very useful feature called **boolean indexing**: you filter an array using another array of `True`/`False` values.

Assume:

```python
bmi = np.array([21.5, 24.8, 27.3, 22.0])
```

1. Create a boolean mask:
```python
over_23 = bmi > 23
# np.array([False, True, True, False])
```

2. Use it to filter:
```python
bmi_over_23 = bmi[over_23]
# contains only the elements where the mask is True
```

This pattern (comparison → boolean array → subsetting) is exactly what you’ll later use for “century masks” on your 2D table.

---

## 6. 2D NumPy arrays

### 6.1. What is a 2D array?

A **2D NumPy array** is like a numerical spreadsheet:

- data is organised in **rows** and **columns**,
- internally it is still a single `numpy.ndarray` object.

You create it from a list of lists:

```python
import numpy as np

data = [
    [1.73, 65.4],
    [1.68, 59.2],
    # ...
]

np_2d = np.array(data)
```

Each inner list becomes one row of the 2D array.

### 6.2. The `shape` attribute

Every NumPy array has a `shape` attribute describing its dimensions:

```python
np_2d.shape      # for example: (2, 5)
```

- This means 2 rows and 5 columns.
- `shape` is an **attribute**, so you do **not** use parentheses (`np_2d.shape`, not `np_2d.shape()`).

The “single‑data‑type” rule still applies to 2D arrays: all cells share the same type.

---

## 7. Selecting data from 2D arrays

There are two main indexing styles.

### 7.1. Double brackets (like a list of lists)

This mirrors basic Python lists:

```python
value = np_2d  # row 0, then column 2
```


### 7.2. Comma notation (recommended in NumPy)

More natural in NumPy:

```python
value = np_2d  # same value as above
```

Before the comma → row index,
after the comma → column index.

#### Slicing in 2D

You can slice rows, columns, or blocks:

```python
row_1_all_cols = np_2d[1, :]     # entire second row
all_rows_col_0 = np_2d[:, 0]     # entire first column
middle_block   = np_2d[1:3, 1:3] # rows 1–2, columns 1–2 (upper bound excluded)
```

The slicing rules are the same as for 1D lists: the end index is **exclusive**.

---

## 8. NumPy: basic statistics

### 8.1. Why summary statistics?

With thousands of observations you cannot “eyeball” the raw numbers.
The first step in any analysis is to compute **summary statistics** – a quick sanity check that tells you whether the data looks reasonable.

NumPy provides fast numerical functions for this.

### 8.2. Core statistical functions

Some of the most important ones:

- `np.mean(arr)` – arithmetic mean (average).
- `np.median(arr)` – median, robust to extreme outliers.
- `np.std(arr)` – standard deviation, measures spread around the mean.
- `np.corrcoef(x, y)` – correlation coefficient(s) between two variables.
- `np.sum(arr)` – sum of all elements.
- `np.sort(arr)` – sorted copy of the array.


### 8.3. Using them with a 2D array

Assume `np_city` is a 2D array where:

- column 0 = height,
- column 1 = weight.

First select the columns:

```python
heights = np_city[:, 0]
weights = np_city[:, 1]
```

Then compute statistics:

```python
mean_height   = np.mean(heights)
median_height = np.median(heights)
std_weight    = np.std(weights)
corr_hw       = np.corrcoef(heights, weights)
total_weight  = np.sum(weights)
sorted_height = np.sort(heights)
```

These give you:

- typical values (mean, median),
- how spread out the data is (standard deviation),
- whether two variables move together (correlation),
- quick global properties (sum, sorted values).

---

## 9. Why NumPy instead of pure Python?

Although base Python has some numeric helpers (like `sum()`), NumPy is crucial because:

- it enforces a **single data type** per array, enabling highly optimised low‑level code,
- it supports true **element‑wise and vectorised operations**,
- it is the numerical backbone for other data‑science libraries (pandas, scikit‑learn, etc.).

