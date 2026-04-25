# Logic, Control Flow, and Filtering

## Overview
This note covers three connected ideas in intermediate Python: **comparison and boolean logic**, **control flow with conditional statements**, and **filtering tabular data with Pandas**. Together, these tools let code make decisions instead of running the same way every time.

## Comparison Operators
Comparison operators answer a simple question: **how do two values relate to each other?** The result is always a Boolean value, either `True` or `False`.

Common comparison operators:

- `<` means *less than*
- `>` means *greater than*
- `<=` means *less than or equal to*
- `>=` means *greater than or equal to*
- `==` means *equal to*
- `!=` means *not equal to*

Examples:

```python
2 < 3      # True
2 == 3     # False
3 <= 3     # True
```

These operators work on numbers, variables, and also strings. Strings are compared alphabetically, so:

```python
"carl" < "chris"   # True
```

A common beginner mistake is comparing values of incompatible types, such as an integer and a string, which causes an error.

```python
3 < "chris"   # Error
```

## Boolean Operators
Once comparisons produce `True` or `False`, Boolean operators let you combine them.

The three most important Boolean operators are:

- `and` — returns `True` only if **both** conditions are `True`
- `or` — returns `True` if **at least one** condition is `True`
- `not` — reverses a Boolean value[ file:5]

Examples:

```python
x = 12
x > 5 and x < 15    # True

y = 5
y < 7 or y > 13     # True

not True            # False
```

## Boolean Logic in NumPy
With NumPy arrays, standard `and`, `or`, and `not` do **not** work element by element. Instead, NumPy provides special functions for array-wise logic.

Use:

- `np.logical_and()`
- `np.logical_or()`
- `np.logical_not()`

Example:

```python
import numpy as np
bmi = np.array([21.5, 22.3, 24.1, 19.8])

np.logical_and(bmi > 21, bmi < 22)
```

This is useful because NumPy compares each element separately, which is called **element-wise** behavior.

## Control Flow: `if`, `elif`, `else`
Control flow means letting Python choose different actions depending on conditions. The main tools are `if`, `elif`, and `else`.

### `if`
Use `if` when code should run only when a condition is true.

```python
z = 4
if z % 2 == 0:
    print("z is even")
```

Important syntax rules:

- Put a colon `:` at the end of the condition line
- Indent the code block below it
- If the condition is `False`, Python skips that block[ file:5]

### `else`
Use `else` for the fallback case.

```python
z = 5
if z % 2 == 0:
    print("z is even")
else:
    print("z is odd")
```

### `elif`
Use `elif` when there are multiple possible conditions.

```python
z = 3
if z % 2 == 0:
    print("divisible by 2")
elif z % 3 == 0:
    print("divisible by 3")
else:
    print("something else")
```

Python checks conditions **from top to bottom** and stops at the **first** one that is `True`. This means order matters.

## Filtering Pandas DataFrames
Filtering means keeping only the rows that meet a condition. In Pandas, this usually happens in three steps:

1. Select a column.
2. Build a Boolean condition.
3. Use that Boolean result to subset the DataFrame.

Example:

```python
is_huge = brics["area"] > 8
brics[is_huge]
```

A shorter one-line version is:

```python
brics[brics["area"] > 8]
```

This works because the Boolean Series acts like a **mask**: rows with `True` stay, and rows with `False` are removed.

## Combining Conditions in Pandas
To filter with more than one condition, use NumPy logical functions.

Example: keep only rows where area is between 8 and 10.

```python
import numpy as np

brics[np.logical_and(brics["area"] > 8,
                     brics["area"] < 10)]
```

Using plain `and` on whole columns does not work correctly, because Pandas columns behave like arrays.

## Key Takeaways
- Comparison operators return `True` or `False`.
- Boolean operators combine conditions.
- NumPy arrays need `np.logical_*` functions for element-wise logic.
- `if`, `elif`, and `else` control which code runs.
- Pandas filtering uses Boolean masks to keep selected rows.

## Quick Mental Model
Think of this whole topic as **teaching Python to make choices**. Comparison operators ask questions, Boolean operators combine questions, `if` statements decide what to do next, and DataFrame filtering keeps only the rows that satisfy the rules.
