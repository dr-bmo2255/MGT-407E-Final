# MGT 407E Final: Diamond Price Regressions

An interactive OLS regression tool for the Part B diamond pricing question.

## Files

| File | What it is |
|---|---|
| `diamonds_regression_tool.html` | The tool. A single self-contained page with both datasets embedded. Download it and open it in any browser. |
| `data/diamonds.csv` | The original dataset (53,940 rows). |
| `data/diamonds_clean_v12.csv` | The cleaned dataset (52,893 rows, adds `calculated_depth`). |
| `src.html` | Source for the tool, with a `/*DATA*/` placeholder where `data.js` is inserted. |
| `data.js` | Both datasets packed for embedding in the tool. |
| `price_vs_table.png`, `price_vs_depth.png` | Single-variable scatterplots with their OLS lines (cleaned data). |

## What the tool does

- A switch picks the original or the cleaned dataset.
- Every variable has an on/off switch. Cut, color and clarity enter as 0/1 dummy variables, each with a selectable base (omitted) level.
- Depth and x/y/z are never used in the same regression. On the cleaned data, depth means `calculated_depth = 100 × z / ((x + y) / 2)`.
- The regression table follows the course format: coefficients, standard errors below them, t-statistics (in italics) below those, then Observations, R-squared, Std Dev of Dep Var and Sample. Up to 6 regressions sit side by side.
- The scatterplot lets you choose the variable on each axis. When price is on the vertical axis, each regression's predicted-price line is drawn, either on one plot or on separate plots.
- Estimates are standard (non-robust) OLS, rounded to the hundredths. They were checked against Python statsmodels.

## Cleaning steps (original → cleaned)

1. 146 exact duplicate rows removed.
2. Three extreme y/z values shifted one decimal place; two of those rows were then removed.
3. Zeros in x, y, z set to missing.
4. 3 rows where z equals carat removed.
5. 397 rows that were identical to another row except for price removed.
6. 467 rows that were identical to another row except for one column removed.
7. 10 rows in the tails of table removed.
8. 12 rows with an x/y gap above 0.5 removed.
9. 10 rows with extreme calculated depth removed. The next 5 lowest and 5 highest calculated depth values were then set to missing.
