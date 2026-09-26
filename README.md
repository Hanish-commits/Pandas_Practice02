# Pandas Practice

Hands-on Pandas exercises worked through in a Jupyter notebook, using a small
sales dataset with intentionally missing values.

## Structure

```
data/        raw dataset(s) used by the notebooks
notebooks/   worked exercises, numbered in order
docs/        exercise questions and review notes
```

## Setup

```bash
pip install pandas numpy jupyter
```

Open a notebook from `notebooks/` and run it from that folder — data paths
are relative (`../data/...`).

## Exercises

| Notebook | Topic |
|---|---|
| [`01_pandas_exercise.ipynb`](notebooks/01_pandas_exercise.ipynb) | DataFrame inspection, filtering, missing values, grouping, pivot tables |
| [`02_pandas_exercise.ipynb`](notebooks/02_pandas_exercise.ipynb) | Series vs DataFrame selection, string cleaning, duplicates, dtype conversion, dates |

Full question list (exercise 1): [`docs/questions.md`](docs/questions.md)
Review notes (exercise 1): [`docs/feedback.md`](docs/feedback.md)
Lessons learned (exercise 2): [`docs/lessons-learned.md`](docs/lessons-learned.md)
