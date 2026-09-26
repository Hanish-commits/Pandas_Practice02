# Pandas Learning Review

A personal revision note from my Pandas practice. It records the mistakes I made, why they happened, and the patterns I want to remember. The examples use a retail orders DataFrame called `df`.

## What I’m already doing well

- Filtering rows with boolean conditions, such as `df[df["country"] == "India"]`.
- Combining conditions with `&` when both conditions must be true.
- Selecting columns and grouping data with `groupby`.
- Using common aggregations such as `sum`, `mean`, and `count`.
- Creating calculated columns and converting values with Pandas conversion functions.
- Trying a solution, reading the error or feedback, and adjusting the code.

## Mistakes and lessons

### 1. Selecting a Series versus a DataFrame

I first selected one column like this:

```python
df["product"]
```

This returns a **Series**. For a one-column **DataFrame**, use a list of column names:

```python
df[["product"]]
```

The extra pair of brackets matters because the inner list tells Pandas to return a DataFrame.

### 2. Selecting more columns than the question asked for

For a question asking for one column, I tried selecting two columns. The code was valid, but it didn’t match the requested output. Before coding, identify exactly which columns and result shape the question asks for.

```python
# Three columns, returned as a DataFrame
df[["order_id", "product", "sales"]]
```

### 3. Checking the exact values before filtering or replacing

I tried to replace `"US"`, but the dataset’s value was `"USA"`. Exact string comparisons and replacements only match the value that is actually present.

```python
# Inspect the values first
print(df["country"].unique())

# Then replace the exact value
df["country"] = df["country"].replace("USA", "United States")
```

### 4. Confusing renaming labels with replacing data values

I tried using `.rename()` to change a country value. `rename` changes index or column labels; it does not replace values in the cells. Use `.replace()` on the column for cell values.

```python
df["country"] = df["country"].replace("USA", "United States")
```

### 5. Checking missing values in the wrong column

For a question about missing customer names, I checked `customer_id`. The method was appropriate, but I applied it to the wrong column. Match the column in the code to the field named in the question.

```python
# Find rows where customer_name is missing
df[df["customer_name"].isna()]
```

### 6. Remembering exact capitalization in conditions

The return values were `"Yes"` and `"No"`, so checking for lowercase `"yes"` would not match. Inspect categories before writing a string condition.

```python
print(df["returned"].unique())
```

With `query`, use `and` / `or` for logical combinations:

```python
df.query("returned == 'Yes' or rating < 4")
```

With ordinary boolean indexing, use `&` / `|` and put each condition in parentheses:

```python
df[(df["returned"] == "Yes") | (df["rating"] < 4)]
```

### 7. Using the right sort direction syntax

I put asterisks around `False`, which is not valid Python syntax. Boolean values are written without asterisks.

```python
df.sort_values("sales", ascending=False)
```

Also, sorting `df["sales"]` sorts only the Series. Use `df.sort_values(...)` when I want complete rows ordered by sales.

### 8. Checking data types before aggregating

The `quantity` column included the string `"unknown"`. Summing a text column may concatenate strings or fail to produce a numeric total. Convert the values first; `errors="coerce"` turns invalid entries into missing values.

```python
df["quantity"] = pd.to_numeric(df["quantity"], errors="coerce")
df.groupby("category")["quantity"].sum()
```

### 9. Distinguishing cleaning a string from standardizing it

`.str.strip()` removes whitespace, but it does not standardize capitalization. For title-style category names, chain the operations:

```python
df["category"] = df["category"].str.strip().str.title()
```

`.str.capitalize()` only capitalizes the first character of the whole string, while `.str.title()` capitalizes the start of each word.

### 10. Understanding what counts as a duplicate

`df.duplicated()` checks the complete row by default. Repeated customer names are not necessarily duplicate orders: one customer can place multiple orders. If the order ID defines a duplicate transaction, check that field explicitly.

```python
# Show every row involved in a repeated order_id
df[df.duplicated(subset="order_id", keep=False)]

# Keep the first row for each order_id
df_clean = df.drop_duplicates(subset="order_id", keep="first")
```

### 11. Avoiding blanket fills across mixed data types

I filled every missing cell with the string `"Unknown"`. This can make numeric columns such as `sales`, `cost`, and `rating` contain text, complicating calculations. Fill only the column where that label makes sense.

```python
df["returned"] = df["returned"].fillna("Unknown")
```

For experiments, keep an untouched source copy:

```python
raw = df.copy()
working = raw.copy()
```

### 12. Converting both sides of a date calculation

I converted the reference date to a timestamp, but the `order_date` column was still text. A datetime cannot be subtracted from strings. Convert the column and the reference date before subtracting.

```python
df["order_date"] = pd.to_datetime(df["order_date"], errors="coerce")
reference_date = pd.to_datetime("2024-03-01")

df["days_since_order"] = (reference_date - df["order_date"]).dt.days
```

Invalid dates become `NaT`, and their day differences remain missing.

## My checklist before running Pandas code

1. **Output:** Do I need a Series, DataFrame, or scalar result?
2. **Column:** Am I using the exact column named in the question?
3. **Values:** Have I checked the actual spelling and capitalization with `.unique()` or `value_counts()`?
4. **Type:** Is the column numeric, text, or datetime as required for this operation?
5. **Missing data:** What should happen to missing or invalid values?
6. **Scope:** Am I changing one column or the whole DataFrame?
7. **Rows:** If sorting or filtering, do I need the complete rows or only one Series?
8. **Source copy:** Should I work on a copy so I can recover the original data?

## Learning focus

The main areas I want to keep practicing are:

- Choosing the correct result shape when selecting columns.
- Inspecting actual values before filtering or replacing text.
- Understanding Pandas data types and converting them before calculations.
- Handling missing values at the appropriate column level.
- Distinguishing row duplicates from repeated values in a single column.
- Translating the wording of a question into the exact requested output.

## Practice setup

```python
import pandas as pd

# Start from the original data and keep a working copy
raw = pd.DataFrame(data)
df = raw.copy()
```
