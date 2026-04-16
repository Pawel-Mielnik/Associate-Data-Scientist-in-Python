# Dictionaries and Pandas DataFrames

This note summarizes two core building blocks for data work in Python: **dictionaries** and **Pandas DataFrames**.  
Dictionaries let you map keys to values efficiently, while DataFrames give you an Excel‑like table inside Python.

---

## 1. Python dictionaries

### 1.1 Why lists are not always enough

Imagine you have two separate lists:

```python
countries = ["Spain", "France", "Italy"]
population_millions = [47.4, 67.4, 58.9]
```

To find the population of Italy, you must:

1. Find the position of `"Italy"` in `countries`.
2. Use that index to look up the value in `population_millions`.

This works, but it is fragile and clumsy once your data grows.

### 1.2 Dictionary: key → value

A **dictionary** connects a *key* directly to a *value*, like a real dictionary connects a word to its definition.

```python
world_pop = {
    "Spain": 47.4,
    "France": 67.4,
    "Italy": 58.9,
}
```

Now you can access data directly:

```python
world_pop["Italy"]  # 58.9
```

No searching for indices, no manual synchronization of multiple lists.

**Why dictionaries are awesome:**
- **Readable**: `world_pop["Italy"]` reads like plain English.
- **Fast**: Python can find a key very quickly even in a huge dictionary.

### 1.3 Rules for dictionary keys

Dictionaries have two important rules for keys:

- **Uniqueness**: Each key can appear only once.  
  If you assign the same key twice, the last value wins.
- **Immutability**: Keys must be immutable (cannot change).  
  Good keys: strings, integers, booleans, tuples.  
  Bad keys: lists, other mutable objects.

Example:

```python
# add a new entry
world_pop["Portugal"] = 10.4

# update an existing entry
world_pop["Italy"] = 59.1  # overwrites the old value

# delete an entry
del world_pop["Portugal"]
```

Before you use or delete a key, it is often safer to check if it exists:

```python
if "Spain" in world_pop:
    print(world_pop["Spain"])
```

---

## 2. When to use a list vs a dictionary

Very rough rule of thumb:

| Question                          | Use this        |
|----------------------------------|-----------------|
| “Give me the 10th element.”      | **List**        |
| “Give me the value for 'Italy'.” | **Dictionary**  |

- Use a **list** when order matters and you work with positions (0, 1, 2, …).  
- Use a **dictionary** when you want to look things up by **name** (a key) instead of by index.

---

## 3. Pandas DataFrames

### 3.1 Why Pandas on top of NumPy

NumPy arrays work best when **all values have the same type** (all floats, all ints, etc.).  
Real‑world data is usually mixed:

- country name – text,
- population – integer,
- area – float.

Pandas solves this by providing the **DataFrame**, a 2D table structure that can store mixed types in different columns.

### 3.2 What is a DataFrame?

A DataFrame is a **table of data**:

- **Rows** = observations (for example, one row per country).
- **Columns** = variables/features (for example, capital, population, area).
- Both rows and columns have labels (index, column names).

It is very similar to:

- a sheet in Excel,
- a table in SQL,
- but living directly in Python with powerful methods for analysis.

---

## 4. Building a DataFrame from a dictionary

The most common pattern in small examples is:

1. Put your data into a dictionary of lists.
2. Pass that dictionary to `pd.DataFrame()`.

```python
import pandas as pd

data = {
    "country": ["Spain", "France", "Italy"],
    "capital": ["Madrid", "Paris", "Rome"],
    "population_millions": [47.4, 67.4, 58.9],
}

countries = pd.DataFrame(data)
print(countries)
```

Here:

- dictionary **keys** (`"country"`, `"capital"`, `"population_millions"`) become column names,
- each list becomes one column’s values.

### 4.1 Setting custom row labels (index)

By default, Pandas uses integer row labels: 0, 1, 2, …  
You can replace them with something more meaningful, for example ISO country codes:

```python
row_labels = ["ES", "FR", "IT"]
countries.index = row_labels
print(countries)
```

Now the index shows `ES`, `FR`, `IT` instead of 0, 1, 2.

---

## 5. Creating a DataFrame from a CSV file

In real projects, you will rarely type all data by hand.  
Most of the time, it will come from a **CSV file** (comma‑separated values).

```python
import pandas as pd

# Suppose the first column contains row labels (e.g. ES, FR, IT)
countries = pd.read_csv("countries.csv", index_col=0)
```

- `read_csv` loads the file into a DataFrame.
- `index_col=0` tells Pandas that the first column in the CSV should be used as the row index, not as a regular data column.

---

## 6. Selecting data from a DataFrame

There are three main ways to access data inside a DataFrame:

1. Square brackets `[]`
2. `.loc` – label‑based
3. `.iloc` – position‑based

### 6.1 Square brackets for quick column access

```python
# Series (one-dimensional)
countries["country"]

# DataFrame with a single column (still looks like a table)
countries[["country"]]

# Multiple columns at once
countries[["country", "capital"]]
```

For rows, simple slicing also works:

```python
# rows from position 1 up to (but not including) 3
countries[1:3]
```

### 6.2 `.loc` — select by label

`.loc` lets you select by **row and column labels**.

```python
# single row by index label
countries.loc["FR"]

# multiple rows and columns
countries.loc[["ES", "IT"], ["country", "capital"]]

# all rows, selected columns
countries.loc[:, ["country", "population_millions"]]
```

Think: “I know the **names**.”

### 6.3 `.iloc` — select by integer position

`.iloc` works like `.loc`, but uses integer positions instead of labels.

```python
# second row (index 1)
countries.iloc

# rows 0–2, columns 0–1
countries.iloc[0:3, 0:2]
```

Think: “I know the **positions** (first row, second column, etc.).”

---