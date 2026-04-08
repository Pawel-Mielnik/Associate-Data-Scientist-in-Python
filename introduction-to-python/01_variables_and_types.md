# Variables and Data Types in Python

## 1. What is a variable?

A **variable** is a named box where you store a value so you can reuse it later.

- You create a variable with the `=` sign.
- Python remembers the value under the given name.
- When you type the name, Python gives you the stored value.

```python
height = 1.79      # in meters (float)
weight = 68.7      # in kilograms (float)

bmi = weight / height ** 2
bmi
```

### Why variables are useful (reproducibility)

If you change the value in **one place**, all calculations that use this variable will automatically use the new value.

```python
weight = 72.0      # updated weight
bmi = weight / height ** 2
bmi
```

This is powerful, because you can:

- update inputs once,
- rerun the code,
- get new results without editing every line.

### Naming rules (short version)

- Names are **case‑sensitive**: `Height` and `height` are two different variables.
- Use letters, digits and `_` (underscore), but **do not** start with a digit.
- Good style: use lowercase with underscores, e.g. `body_mass_index`, `user_age`.

```python
userAge = 25      # works, but not recommended
user_age = 25     # recommended (snake_case)
```

---

## 2. Basic data types in Python

Every value in Python has a **type**.  
The type defines how the value is stored and how operators (like `+`) behave with it.

We will focus on 4 core types:

- `int`  – integer (whole number)
- `float` – floating‑point number (decimal)
- `str` – string (text)
- `bool` – boolean (True/False)

You can always check the type with `type(value)`.

```python
type(5)           # int
type(1.79)        # float
type("Python")    # str
type(True)        # bool
```

### 2.1. Integers – `int`

**Idea:** whole numbers, without decimal part.

Examples:

```python
age = 25
year = 2026
temperature_change = -3

type(age)      # int
```

Typical operations:

```python
10 + 5      # 15
10 - 5      # 5
10 * 5      # 50
10 // 3     # 3  (integer division)
10 % 3      # 1  (remainder)
```

### 2.2. Floating‑point numbers – `float`

**Idea:** real numbers with a decimal point.

Examples:

```python
height = 1.79
weight = 68.7
pi = 3.14159

type(height)   # float
```

Typical operations (same as for `int`, but with decimals):

```python
bmi = weight / height ** 2
bmi
```

### 2.3. Strings – `str`

**Idea:** text, anything inside quotes.

You can use single or double quotes:

```python
first_name = "John"
last_name = 'Doe'
language = "Python"

type(first_name)   # str
```

String operations:

```python
full_name = first_name + " " + last_name   # concatenation
greeting = "Hello " * 3                    # repetition
```

Accessing characters (indexing starts from 0):

```python
language   # 'P'
language   # 'y'
```

### 2.4. Booleans – `bool`

**Idea:** logical value – only `True` or `False`.

Booleans often come from comparisons:

```python
is_student = True
is_adult = age >= 18          # True if age is 18 or more

type(is_student)              # bool
```

Comparison examples:

```python
5 > 3          # True
5 < 3          # False
5 == 5         # True
5 != 5         # False
```

Booleans are also used with logical operators:

```python
has_ticket = True
has_id = False

can_enter = has_ticket and has_id   # False
```

---

## 3. Operator `+` depends on the type

The `+` operator behaves **differently** depending on the data type.

### Numbers (`int`, `float`)

For numbers, `+` means **addition**.

```python
2 + 3        # 5
1.5 + 2.5    # 4.0
```

### Strings (`str`)

For strings, `+` means **concatenation** (joining text).

```python
"Hello" + " " + "World"   # 'Hello World'
```

### Mixing types – common error

If you try to combine a string and a number directly, Python raises an error:

```python
age = 25
message = "Your age is " + age
# TypeError: can only concatenate str (not "int") to str
```

You must convert the number to a string:

```python
message = "Your age is " + str(age)
message    # 'Your age is 25'
```

---

## 4. Converting between types (casting)

Sometimes you need to change the type of a value.

### Number ↔ number

```python
x = 5               # int
float_x = float(x)  # 5.0

y = 3.9
int_y = int(y)      # 3  (decimals are cut off, not rounded)
```

### String ↔ number

```python
age_str = "30"
age_int = int(age_str)        # 30

height_str = "1.79"
height_float = float(height_str)   # 1.79
```

If the string is not a valid number, conversion fails:

```python
int("abc")   # ValueError
```

---

## 5. Small practice examples

You can use these as mini‑exercises or test cells.

### 5.1. BMI calculator

```python
height = 1.79
weight = 68.7

bmi = weight / height ** 2
bmi
```

### 5.2. Simple profile

```python
name = "Alice"
age = 28
is_student = False

profile = name + " is " + str(age) + " years old."
profile
```

### 5.3. Temperature check

```python
temperature = 22.5
is_hot = temperature > 25

is_hot
type(is_hot)
```