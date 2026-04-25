# Case Study: Hacker Statistics

A concise, GitHub-ready note based on the **"Python Intermediate - Complete"** material, focused on the **Hacker Statistics** case study.

## What is Hacker Statistics?
**Hacker Statistics** means using **simulation** to estimate the probability of an event instead of solving it only with formulas.
The main idea is simple: if a problem is hard to calculate directly, you can let the computer repeat the experiment many times and observe the results.

## Core intuition
Think of it like this: instead of asking *"What should the probability be in theory?"*, you ask *"What happens if I play this game 10,000 times?"*.
With enough repetitions, the simulated result becomes a very good approximation of the real probability.

## The staircase problem
In the case study, the scenario is a game on the **Empire State Building stairs**.
You roll a die **100 times**, and your position changes according to the result.

Rules from the note:
- If the die shows **1 or 2**, you go **one step down**.
- If the die shows **3, 4, or 5**, you go **one step up**.
- If the die shows **6**, you roll again and go up by the new value.
- You can never go below **step 0**.
- There is also a **0.1% chance** that you trip and fall back to **0**.

The question is: **what is the probability of reaching step 60?**.

## Why simulation is used
This is a good example of a process with **many random steps**.
Because the outcome depends on repeated randomness, simulation is easier and more intuitive than building the full mathematical solution by hand.

## Random numbers in NumPy
The case study uses **NumPy's random tools** to simulate chance.
Two important functions from the note are **`np.random.seed()`** and **`np.random.randint()`**.

```python
import numpy as np

np.random.seed(123)
coin = np.random.randint(0, 2)
```

### Why `seed()` matters
A **seed** fixes the random number generator so you can get the **same random results again**.
That is useful for debugging, learning, and making your notebook reproducible.

## Simple coin example
Before the stairs simulation, the note introduces a small example with a coin toss.
The goal is to show how random outcomes can be generated in Python.

```python
import numpy as np

np.random.seed(123)
coin = np.random.randint(0, 2)

if coin == 0:
    print("heads")
else:
    print("tails")
```

## Random walk
A **random walk** is a process where each new position depends on the previous one plus some random change.
That is the central concept behind the Hacker Statistics case study.

In plain English:
- you start somewhere,
- chance changes your position,
- then the next move starts from the new position,
- and this repeats many times.

## Example: counting tails
The note explains random walk with a simpler example: counting tails over repeated coin tosses.
Each new value depends on the previous total, which makes it a step-by-step process.

```python
import numpy as np

np.random.seed(123)
tails = [0]

for x in range(10):
    coin = np.random.randint(0, 2)
    tails.append(tails[x] + coin)

print(tails)
```

### What happens here?
- `tails` starts at `[0]`.
- Each toss adds either **0** or **1**.
- The next result always depends on the previous one.

That is exactly the logic of a random walk.

## Repeating the experiment many times
One simulation run gives only **one possible outcome**.
To understand the full behavior, you repeat the process many times and collect the final results.

The note shows this idea with repeated coin-toss experiments.
Each game has 10 tosses, and the final number of tails is stored.

```python
import numpy as np

np.random.seed(123)
final_tails = []

for i in range(100):
    tails = [0]
    for x in range(10):
        coin = np.random.randint(0, 2)
        tails.append(tails[x] + coin)
    final_tails.append(tails[-1])
```

## Distribution
A **distribution** shows how often different outcomes happen.
Instead of looking at one result, you now look at the pattern across many simulations.

For example, after many coin-toss games, you can ask:
- How often do we end with **5 tails**?
- How often do we end with **8 tails**?

This is the bridge from **single random outcome** to **probability estimation**.

## Histogram
The note uses a **histogram** to visualize the distribution of simulation results.
A histogram makes it easy to see which outcomes happen often and which are rare.

```python
import matplotlib.pyplot as plt

plt.hist(final_tails, bins=10)
plt.show()
```

### What the histogram shows
- The **x-axis** shows possible outcomes, such as the final number of tails.
- The **y-axis** shows how often each outcome appeared.
- More simulations usually make the shape smoother and more stable.

The note points out that **100 simulations** can look rough, **1,000** looks better, and **10,000** gets much closer to the expected theoretical shape.

## Applying this to the stairs game
The same logic is used for the Empire State Building problem.
Instead of tracking tails, you track the **step position** after each die roll.

A full approach would be:
1. Simulate one walk of 100 die rolls.
2. Store the final or maximum step reached.
3. Repeat that simulation thousands of times.
4. Estimate the probability of reaching step 60 by counting how often it happens.

## Why this matters in data science
This case study teaches a very important habit: **when exact math is hard, simulate**.
That mindset is useful in probability, experimentation, risk analysis, and many real-world systems with uncertainty.

## Key tools used
| Tool | Purpose |
|---|---|
| `np.random.seed()` | Makes random results reproducible. |
| `np.random.randint()` | Generates random integers. |
| `for` loop | Repeats the simulation many times. |
| list | Stores the path or final outcomes. |
| `plt.hist()` | Visualizes the distribution of results. |

## Minimal mental model
Use this simple way to remember the topic:

- **Randomness** gives different outcomes each time.
- **Random walk** means each step depends on the previous step.
- **Simulation** means repeating the process many times.
- **Distribution** means looking at the pattern of all results.
- **Hacker Statistics** means estimating probability through repeated experiments.

## Final takeaway
**Hacker Statistics is about learning probability by simulation**.
Instead of solving everything with equations, you model the random process in code, run it many times, and use the results to estimate what is likely to happen.
