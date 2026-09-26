# Pandas Learning Feedback

## Learning request recorded

The learner asked for hands-on Pandas revision using a DataFrame, with questions first and answers at the end. They are working in PyCharm and asked that the dataset be available as a file, with questions and feedback kept separately.

## Strengths observed from submitted answers

- DataFrame inspection: used `head()`, `shape`, `dtypes`, and `isna().sum()` correctly.
- Missing-value handling: used `fillna()` with a fixed value and a median.
- Boolean filtering: filtered by status and combined conditions with `&`.
- Calculated columns: correctly multiplied quantity by price and applied discounts.
- Grouping and aggregation: correctly calculated sums/counts by city and product.
- Sorting and top result: correctly sorted descending and selected the top row. The correct maximum was order 1001; the earlier feedback naming order 1004 was mistaken.
- Pivot tables: used city and product axes and filled empty combinations.
- Monthly aggregation: correctly filtered shipped rows, grouped by month, and summed totals after creating a month column.

## Topics to keep practicing

- Use `.loc[row_condition, columns]` when selecting both rows and columns.
- Use `ascending=True` for oldest-to-newest sorting and sort the full DataFrame to keep row values together.
- For grouped means, filter the rows first, then group and call `.mean()`.
- Create derived columns such as `month` before grouping by them.
- Check column names carefully to avoid spelling errors.
- Identify missing rows before filling when you need to report which records were affected.

## Current feedback summary

The learner is strongest so far in filtering, vectorized column calculations, and grouped summaries. These observations are based on the answers submitted in this practice session; future exercises can refine the assessment.
