# Pandas Revision Questions

Load `pandas_sales_dataset.csv` into a DataFrame named `df`. The CSV includes missing values intentionally for practice.

```python
import pandas as pd

df = pd.read_csv("pandas_sales_dataset.csv")
```

## Questions

1. Display the first five rows. How many rows and columns does `df` have?
2. Show each column’s data type and count missing values in each column.
3. Convert `date` to datetime, then sort the DataFrame by date, oldest first.
4. Select `order_id`, `city`, and `product` for orders from Mumbai.
5. Find shipped orders with a quantity of at least 2.
6. Fill missing `quantity` values with 1 and missing `unit_price` values with the median. Which orders had missing values? Identify them before filling.
7. Add a `gross_total` column equal to `quantity * unit_price`.
8. Add a `net_total` column after discount: `gross_total * (1 - discount_pct)`. Round to 2 decimal places.
9. Calculate total net sales by city across all statuses. Then calculate shipped-only net sales by city.
10. Count the number of orders per product.
11. Find the average `net_total` for shipped orders, grouped by product.
12. Find the order with the highest `net_total`. Return its `order_id`, `product`, and `net_total`.
13. Create a pivot table with city as rows, product as columns, and the sum of `net_total` as values. Fill missing combinations with 0.
14. Calculate total `net_total` for shipped orders. In one sentence, explain why this might be more useful than including every status.
15. **Challenge:** Add a `month` column from `date`, then calculate shipped net sales by month.

## Working notes

Write your answers in a separate Python file or notebook. When finished, send your code or answers by question number for feedback.
