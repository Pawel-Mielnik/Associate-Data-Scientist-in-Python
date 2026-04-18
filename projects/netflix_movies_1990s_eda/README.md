# Netflix Movies in the 1990s – EDA

This is a small exploratory data analysis (EDA) project based on a real-world project from **DataCamp**.  
The goal is to practice working with pandas, filtering data using boolean masks, and answering simple business-style questions.

## Project description

The dataset (`netflix_data.csv`) contains information about titles available on Netflix, including:

- type (Movie or TV Show),
- title,
- country,
- date added,
- release year,
- duration in minutes,
- genre and description.

In this project I focus only on **movies released in the 1990s**.

## Questions answered

1. **What was the most frequent movie duration in the 1990s?**  
   I filter the data to keep only movies from 1990–1999 and compute the **mode** of the `duration` column.

2. **How many short action movies were released in the 1990s?**  
   A short movie is defined as a movie with a duration of **less than 90 minutes**.  
   Among 1990s movies, I select titles with `genre == "Action"` and `duration < 90`, and count how many such movies there are.

The final results are stored in two variables inside the notebook:

- `duration` – the most common movie duration in minutes,
- `short_movie_count` – the number of short action movies from the 1990s.

## Files

- `notebook.ipynb` – main Jupyter notebook with the analysis.
- `data/netflix_data.csv` – dataset used in this project.
- `images/` *(optional)* – screenshots or plots related to the analysis.

## Tools and libraries

- Python
- pandas
- Matplotlib (for optional visualizations)

## What I practiced here

- Loading CSV data into a pandas DataFrame.
- Filtering data using multiple boolean conditions.
- Selecting columns and computing the mode of a numeric variable.
- Counting rows that satisfy several conditions at once.
- Writing a small, self-contained notebook that can be shared as part of a portfolio.