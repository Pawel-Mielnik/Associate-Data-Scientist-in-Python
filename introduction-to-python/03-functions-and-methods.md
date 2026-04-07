
# Functions, Methods and NumPy – Introduction

## 1. What is a function?

A **function** is a reusable block of code designed to perform a specific task.  
Instead of repeating the same code many times, you wrap it into a function and just call it when needed.

- You give the function some **input(s)** (called *arguments*).
- The function does some work inside (a “black box”).
- It returns an **output** (the result).

You do not need to know how it works internally to use it.

### Built‑in functions (examples)

Python ships with a lot of ready‑made functions:

- `type(x)` – returns the type of `x`.
- `max(seq)` – largest element in a sequence.
- `round(x, ndigits)` – rounds a number.
- `help(obj)` – shows documentation for an object or function.

Example:

```python
heights = [1.72, 1.85, 1.79]
tallest = max(heights)  # 1.85
```


---

## 2. Calling functions and arguments

To **call** a function, you write its **name**, then parentheses with arguments inside:

```python
result = round(1.6789, 2)
```

Here:

- `round` – function name.
- `1.6789` – first argument.
- `2` – second argument (number of decimal places).
- `result` – gets the returned value.


### Positional arguments

Most basic form: arguments are matched to parameters by **position**.

```python
round(1.6789, 2)
# number -> 1.6789
# ndigits -> 2
```


### Optional / default arguments

Some function parameters have **default values** and are optional.

For `round(number, ndigits)`, `ndigits` is optional:

```python
round(1.68)   # 2  (rounded to nearest integer)
```

If you omit `ndigits`, Python uses the default (round to whole number).

---

## 3. Python objects and methods

In Python **everything is an object**: strings, numbers, lists, etc.
Each object has:

- a **type** (e.g. `str`, `float`, `list`)
- a **value**
- a set of **methods** (functions that “belong” to that object)


### Functions vs methods

- **Built‑in function** – independent, you pass data as an argument.
Example: `len(my_list)`, `max(my_list)`
- **Method** – called *on* an object, using **dot notation**.
Example: `my_list.index("item")`, `name.capitalize()`

General syntax:

```python
object.method(arguments)
```


### Examples of methods

Assume:

```python
family = ["Anna", 1.72, "Mark", 1.83, "Nina", 1.64]
sister = "amelia"
```

Some typical methods:

- Lists:
    - `family.index("Mark")` – index of `"Mark"`.
    - `family.count(1.72)` – how many times `1.72` appears.
- Strings:
    - `sister.capitalize()` → `"Amelia"`
    - `sister.replace("a", "aa")` → `"aameliaa"`

> Different types have different methods. `replace()` exists for strings, but not for lists.

### In‑place methods

Some methods **modify the object itself** instead of returning a new one.

Example:

```python
scores = 
scores.append(14)   # scores is now 
```

`append` changes `scores` in place and returns `None`.
You should **not** assign its result to a new variable:

```python
wrong = scores.append(14)  # wrong: wrong will be None
```

Always check whether a method:

- returns a new object (non‑destructive), or
- modifies the existing one in place.

---

## 4. Packages and modules

Python’s standard library does not include every possible tool.
To keep things organised and extensible, Python uses **packages**.

- **Package** – a folder containing multiple Python modules.
- **Module** – a single `.py` file inside a package; it defines functions, classes, etc.

There are thousands of third‑party packages.
For Data Science, some core ones are:

- `numpy` – fast numeric arrays and vectorised computation.
- `matplotlib` – plotting and basic visualisation.
- `scikit-learn` – classical machine learning.


### Installing packages

For packages that are not built‑in, you usually install them with **pip** (in terminal):

```bash
pip install numpy
```

(Or `pip3` depending on your setup.)

---

## 5. Importing packages in Python

To use an installed package in your code, you must **import** it.

### 5.1 Standard import

Most explicit and readable:

```python
import numpy

arr = numpy.array()
```

Pros: always clear where functions come from.

### 5.2 Import with alias (very common)

Shortens the name; **standard practice in Data Science** for NumPy:

```python
import numpy as np

arr = np.array()
```

You still see that `array` comes from NumPy, but the code is less verbose.

### 5.3 Importing specific names (less recommended)

You can import only one function or class directly:

```python
from numpy import array

arr = array()
```

Downside: it is no longer obvious that `array` comes from NumPy and names can clash more easily.
For learning and for larger projects, prefer `import numpy as np`.

