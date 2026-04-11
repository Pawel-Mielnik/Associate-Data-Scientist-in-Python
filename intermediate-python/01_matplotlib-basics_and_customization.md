# Matplotlib – From Basic Plots to Customization

This note summarizes the Matplotlib part of the **Python Intermediate** material – from basic visualization to core customization options.

---

## 1. Why visualization matters

- **Exploration** – helps you understand a dataset and spot patterns or outliers that are hard to see in raw tables.
- **Communication** – lets you share insights in a clear, visual way (e.g. bubble charts combining GDP and life expectancy).

---

## 2. Getting started with Matplotlib

```python
import matplotlib.pyplot as plt
```

- `matplotlib` is the base plotting library in Python.
- `pyplot` is the high‑level interface; by convention we import it as `plt`.

General pattern for all plots:

```python
plt.<plot_function>(...)  # build the figure in memory
plt.show()                # render it on screen
```

---

## 3. Line plots

Used to show **change over time** or across an ordered sequence.

```python
plt.plot(x, y)   # x → horizontal axis, y → vertical axis
plt.show()
```

Key points:

- First argument is the X‑values, second is the Y‑values.
- Great for trends (e.g. world population by year).
- Can be slightly misleading if you have only a few measurements (line suggests continuity between points).

---

## 4. Scatter plots

Used to show the **relationship between two variables** as individual points.

```python
plt.scatter(x, y)
plt.show()
```

- Each point = one observation (e.g. one country).
- Perfect for checking **correlation** (e.g. GDP per capita vs. life expectancy).
- Often more “honest” than line plots, because it shows the actual data points instead of a connected line.

---

## 5. Histograms

Histograms visualize the **distribution** of a numeric variable – how often different values appear.

### 5.1. Intuition

1. **Bins** – split the range of values into intervals (e.g. ages 0–20, 20–40, 40–60).
2. **Counting** – count how many data points fall into each bin.
3. **Bars** – draw a bar per bin; height = count of observations in that bin.

### 5.2. Code

```python
plt.hist(data, bins=10)
plt.show()
```

- `data`: list/array of numbers.
- `bins`: number of bins (default is 10).
  - Too few bins → oversimplified picture.
  - Too many bins → very noisy picture.

### 5.3. Why it’s useful

- Quick **sanity check** for a new dataset – you immediately see skew, concentration and outliers.
- Easy to **compare distributions** (e.g. age distribution in 2010 vs. 2050).

---

## 6. Basic plot customization

Raw plots are rarely enough. Customization makes the plot understandable for someone who sees it for the first time.

### 6.1. Labels and title

```python
plt.xlabel("Year")
plt.ylabel("Population (billions)")
plt.title("World Population Projections")
```

- `xlabel()` – label for the X‑axis.
- `ylabel()` – label for the Y‑axis.
- `title()`  – overall plot title.

These must be called **before** `plt.show()`.

### 6.2. Ticks and tick labels

Control which ticks appear on an axis and how they are displayed.

```python
# Custom tick positions on Y
plt.yticks()

# Custom tick labels
plt.yticks(, ["0", "2B", "4B"])  # B = billions
```

- First argument: numeric positions of ticks.
- Second argument (optional): strings used as labels instead of raw numbers.
- Useful for large scales (thousands, millions, billions) or when you want more human‑friendly labels.

### 6.3. Adding more data

You can extend existing lists and re‑plot to show more context, for example:

```python
years = years_1900 + 
pop   = pop_1900   + [6.1, 6.9, 7.8]

plt.plot(years, pop)
plt.show()
```

This helps highlight long‑term trends (e.g. how sharply population exploded in the 20th century).

---

## 7. Reading and refining your plots

When you think a plot is “done”, ask yourself:

> “Could someone who has never seen this project understand what this plot is about in 5 seconds?”

If the answer is no, you probably need:

- clearer axis labels,
- a better/more informative title,
- simpler or more meaningful ticks.

---

## 8. Quick reference

```python
import matplotlib.pyplot as plt

# Line plot
plt.plot(x, y)

# Scatter plot
plt.scatter(x, y)

# Histogram
plt.hist(data, bins=10)

# Basic customization
plt.xlabel("X label")
plt.ylabel("Y label")
plt.title("My Chart")
plt.yticks(, ["0", "2B", "4B"])

plt.show()
```