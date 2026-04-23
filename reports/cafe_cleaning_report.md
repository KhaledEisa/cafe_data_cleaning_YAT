# Cafe Sales Data Cleaning — Before vs After

## Dataset
- Source (raw): `coffee data/dirty_cafe_sales.csv`
- Notebook: `cafe_clean.ipynb`

## Summary (Before vs After)

| Metric | Before cleaning | After cleaning |
|---|---:|---:|
| Rows | 10,000 | 10,000 |
| Columns | 8 | 9 |
| Total missing cells | 6,826 | 639 |
| Duplicate rows | 0 | 0 |

### Missing values by column

**Before (raw):**
- Location: 3,265
- Payment Method: 2,579
- Item: 333
- Price Per Unit: 179
- Total Spent: 173
- Transaction Date: 159
- Quantity: 138
- Transaction ID: 0

**After (cleaned):**
- Item: 480
- Transaction Date: 159
- All other columns: 0

Notes:
- Numeric fields are fully cleaned and imputed: `Quantity`, `Price Per Unit`, `Total Spent` now have 0 missing.
- `Location` and `Payment Method` are fully filled (0 missing).
- Remaining missingness is limited to `Item` and `Transaction Date`.

## What cleaning was done (high-level)

- Converted numeric columns from messy strings to numeric types and handled parsing failures.
- Imputed missing numeric values (`Quantity`, `Price Per Unit`, `Total Spent`).
- Standardized / filled missing `Payment Method` values.
- Resolved missing/unknown `Location` values by imputing based on the relationship between `Item` and `Location`, then filling any remainder using the overall location distribution.
- Reduced unknown/missing `Item` values using price-based inference.
- Added a helper feature column (`price_key`) to support price-based logic.

## Visualizations (Before vs After)

### 1) Missingness comparison

![](assets/cafe/missingness_before_after.png)

### 2) Numeric distributions (Quantity / Price Per Unit / Total Spent)

![](assets/cafe/numeric_distributions_before_after.png)

### 3) Top categories (Item / Payment Method / Location)

![](assets/cafe/top_categories_before_after.png)

## How to regenerate

- Open `cafe_clean.ipynb` and run all cells.
- Run the final “report export” cell (the one that prints where it saved plots/metrics).

Artifacts written by the export cell:
- `reports/assets/cafe/missingness_before_after.png`
- `reports/assets/cafe/numeric_distributions_before_after.png`
- `reports/assets/cafe/top_categories_before_after.png`
- `reports/cafe_metrics.json`
