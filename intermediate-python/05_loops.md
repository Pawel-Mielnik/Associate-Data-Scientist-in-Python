# Python Loops Notes

A concise, GitHub-ready summary of **Python loops** based on the **"Python Intermediate - Complete"** note.

## What is a loop?
A **loop** is a way to repeat code without copying the same lines again and again.
In practice, loops are useful when you want to process many values, rows, or characters using the same logic.

## `while` loop
A **`while` loop** repeats code **as long as a condition is `True`**.
This is useful when you **do not know in advance** how many repetitions you need.

```python
error = 50

while error > 1:
    error = error / 4
    print(error)
```

### When to use `while`
- Use it when repetition depends on a **condition**.
- Good example: keep running until the error becomes small enough.

### Important danger: infinite loop
If the condition never becomes `False`, the loop will never stop.
That is called an **infinite loop**.

Bad example:

```python
error = 50

while error > 1:
    print(error)
```

The loop above never updates `error`, so it keeps running forever.

## `for` loop
A **`for` loop** goes through each element in a sequence, one by one.
Use it when you already know **what you want to iterate over**, such as a list, string, dictionary, NumPy array, or DataFrame.

```python
fam = [1.73, 1.68, 1.71, 1.89]

for height in fam:
    print(height)
```

### Why `for` is so common
- It is simple and readable.
- It works with many Python data structures.
- It is usually the first choice when you want to process items in order.

## `while` vs `for`
The key difference is **control**.
Use **`while`** when repetition depends on a changing condition, and use **`for`** when you want to iterate through a collection of items.

| Loop type | Best use case |
|---|---|
| `while` | Repeat until a condition becomes `False` |
| `for` | Repeat for each item in a sequence |

## `enumerate()`
Sometimes you need **both the value and its position**.
That is where **`enumerate()`** helps.

```python
fam = [1.73, 1.68, 1.71, 1.89]

for index, height in enumerate(fam):
    print(f"Person {index}: {height} m")
```

### Why use `enumerate()`?
- It gives you the **index**.
- It gives you the **value**.
- It is cleaner than manually counting with another variable.

## Looping through a string
A string is also iterable, which means Python can go through it character by character.

```python
for letter in "family":
    print(letter.capitalize())
```

## Looping through a dictionary
A normal loop over a dictionary gives you only the **keys**.
If you want both the key and the value, use **`.items()`**.

```python
world = {"afghanistan": 30.55, "albania": 2.77}

for country, population in world.items():
    print(country, population)
```

### Key idea
- `for x in my_dict:` -> keys only
- `for k, v in my_dict.items():` -> keys and values

## Looping through NumPy arrays
A **1D NumPy array** can be looped over directly.

```python
import numpy as np

bmi = np.array([21.5, 22.3, 24.1])

for value in bmi:
    print(value)
```

For a **2D NumPy array**, a normal loop gives you rows, not single values.
If you want each individual element, use **`np.nditer()`**.

```python
import numpy as np

meas = np.array([[1.73, 1.68],
                 [65.4, 59.2]])

for val in np.nditer(meas):
    print(val)
```

## Looping through a Pandas DataFrame
A normal loop over a DataFrame returns **column names**, not rows.
If you want to iterate through rows, use **`.iterrows()`**.

```python
for label, row in brics.iterrows():
    print(label)
    print(row)
```

If you want one specific value from each row, you can access it inside the loop.

```python
for label, row in brics.iterrows():
    print(f"{label}: {row['capital']}")
```

## Adding a column inside a loop
You can create or update a column while looping through rows.
However, the note points out that this can be **slow for large DataFrames** because Pandas creates a Series on every iteration.

```python
for label, row in brics.iterrows():
    brics.loc[label, "name_length"] = len(row["country"])
```

## Better alternative: `.apply()`
For many DataFrame tasks, **`.apply()`** is better than writing a loop manually.
It is usually cleaner and faster for column-wise operations.

```python
brics["name_length"] = brics["country"].apply(len)
```

## Quick mental model
Use this simple rule:

- **`while`** = "repeat **until** something changes"
- **`for`** = "repeat **for each** item"
- **`enumerate()`** = "give me **index + value**"
- **`.items()`** = "give me **dictionary key + value**"
- **`np.nditer()`** = "give me **every NumPy element**"
- **`.iterrows()`** = "give me **DataFrame rows**"
- **`.apply()`** = "often better than looping in Pandas"

## Common mistakes
- Forgetting to update the condition in a `while` loop, which creates an infinite loop.
- Using a normal `for` loop on a DataFrame and expecting rows, while Python returns column labels instead.
- Using loops in Pandas when a vectorized method like `.apply()` is a better option.

## Minimal examples

### `while`
```python
x = 3
while x > 0:
    print(x)
    x -= 1
```

### `for`
```python
for n in [1, 2, 3]:
    print(n)
```

### `enumerate()`
```python
for i, n in enumerate([10, 20, 30]):
    print(i, n)
```

### Dictionary
```python
for k, v in {"a": 1, "b": 2}.items():
    print(k, v)
```

## Final takeaway
**Loops help you automate repetition**.
For beginner-friendly Python, the most important thing is to understand **when to use `while` and when to use `for`**, and then learn the most common iteration tools for dictionaries, NumPy, and Pandas.
