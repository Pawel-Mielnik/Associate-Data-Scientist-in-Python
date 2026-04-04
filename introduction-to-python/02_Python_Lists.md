


# Python Lists

## 1. Why do we need lists?

Lists solve the problem of storing many related data points (for example, the heights of all family members) **without** creating a separate variable for each single value.

```python
# Instead of:
alice_height = 1.73
bob_height   = 1.68
carol_height = 1.71
david_height = 1.89

# We use one list:
heights = [1.73, 1.68, 1.71, 1.89]
```


## 2. What is a list?

A **list** is a data structure that gives one name to a collection of values.

- Created with square brackets `[]`.
- Values (elements) inside the brackets are separated by commas.
- The list itself has the data type `list`.

```python
heights = [1.73, 1.68, 1.71, 1.89]
type(heights)  # <class 'list'>
```


## 3. Flexibility of lists in Python

Lists are very flexible in terms of what they can contain.

### 3.1 Different data types

Elements of a list can be of any type: `float`, `int`, `str`, `bool`, or other Python types.

```python
mixed_list = ["Anna", 1.73, True]
```


### 3.2 Lists inside lists

A list can contain other lists (nested lists).
This allows you to build more complex, almost “2D” structures.

```python
family = [
    ["Anna", 1.73],
    ["Mark", 1.89]
]
```

> Because lists can store different data types, they are often used to group related information (for example a person’s name and height).

## 4. List functionality

Like every data type (`int`, `str`, etc.), the `list` type has specific functionality and behavior.
The most important tools are:

- **Subsetting** – selecting elements or parts of a list.
- **Adapting** – modifying, adding, or removing elements.

---

## Subsetting lists

### 1. Indexing

Indexing lets you select a **single element** from a list.
Python uses **indexes** (numbers) placed in square brackets right after the list name.

#### A. Positive indexes (from the beginning)

Python starts counting from **0**:

- First element → index `0`
- Second element → index `1`, and so on

```python
people = ["Anna", 1.73, "Ben", 1.82]

people  # "Anna"
people  # 1.73
people  # 1.82  (the 4th element)
```


#### B. Negative indexes (from the end)

You can also count **backwards** using negative indexes.
This is useful when you want to access elements at the end of the list without knowing its length.

- Last element → index `-1`
- Second from last → `-2`, and so on

```python
people = ["Anna", 1.73, "Ben", 1.82]

people[-1]  # 1.82  (last element)
people[-2]  # "Ben"
```


---

### 2. List slicing

Slicing lets you select **multiple elements at once**, and it returns a **new list**.

#### A. Basic syntax

```python
my_list[start:end]
```

- `start`: index where slicing starts (this element is **included**).
- `end`: index where slicing stops (this element is **excluded**).

> Important rule: slicing stops **before** the `end` index.

```python
people = ["Anna", 1.73, "Ben", 1.82, "Clara", 1.65]

people[2:5]   # ["Ben", 1.82, "Clara"]  → elements with indexes 2, 3 and 4
```


#### B. Omitting `start` or `end`

You can skip `start` or `end` to make slicing shorter:

- If you omit `start`, Python starts from the **beginning** (`0`).
- If you omit `end`, Python goes **to the end** of the list.

```python
people[:4]   # elements with indexes 0, 1, 2, 3
people[3:]   # elements from index 3 to the end
```


---

## Manipulating lists

### 1. Changing list elements

Changing values is done with indexing/slicing and the assignment operator `=`.

#### A. Changing a single element

```python
people = ["Anna", 1.73, "Ben", 1.82]
people = 1.75   # change element at index 1
```


#### B. Changing a slice (part of the list)

```python
people = ["Anna", 1.73, "Ben", 1.82]
people[0:2] = ["Alice", 1.70]  # replaces elements with indexes 0 and 1
```


### 2. Adding and removing elements

#### A. Concatenating lists (adding lists)

For lists, the `+` operator **joins** two lists into a new one.

```python
people = ["Anna", 1.73, "Ben", 1.82]
extended_people = people + ["Tom", 1.80]
# ["Anna", 1.73, "Ben", 1.82, "Tom", 1.80]
```


#### B. Deleting elements

To delete elements from a list, use the `del` keyword with an index (or slice).

```python
people = ["Anna", 1.73, "Ben", 1.82]

del people     # removes element with index 2 ("Ben")
# people is now ["Anna", 1.73, 1.82]
```

> After deletion, all elements to the right move one position to the left, so their indexes change.

---

## Lists under the hood: references and copying

This is a very important and subtle aspect of Python.

### 1. Variables as references

When you create a list:

```python
x = 
```

The variable `x` does **not** store the whole list itself.
It stores a **reference (address in memory)** where the list is actually kept.

#### Copying a reference with `=`

If you “copy” a list with the assignment operator:

```python
y = x
```

you are really copying only the **same reference**:

- Both `x` and `y` point to the **same list** in memory.
- Changing the list through `y` is also visible through `x`.

```python
x = 
y = x        # no real copy

y = 99

print(x)  # 
print(y)  # 
```


### 2. How to properly copy a list (new list in memory)

To create a **new list** in memory with the same values, you must use one of these methods:

#### A. Using `list()`

```python
x = 
y = list(x)
```


#### B. Using slicing

```python
x = 
y = x[:]     # full slice
```

Now `x` and `y` are **two separate lists**.
Changes in `y` do **not** affect `x`:

```python
x = 
y = x[:]     # or list(x)

y = 99

print(x)  # 
print(y)  # 
```


