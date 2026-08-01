# Hotazel Steam: Revenue Forecasting Analysis

A Google Colab notebook that builds and compares five regression models to forecast Hotazel Steam's monthly revenue, using production volume, weather (heating/cooling degree days), and seasonal indicators as predictors.

## Business Question

Hotazel Steam wants a reliable way to forecast monthly revenue using operating data (production volume) and weather-driven demand (heating/cooling degree days). This notebook tests models of increasing complexity to find the one that predicts revenue most accurately on unseen data.

## Data

The notebook reads from a CSV file that must be present in the Colab runtime:

- `AICPA_regressionAnalysisData.csv`

Columns used:
- `date`
- `production`
- `coolDD` (cooling degree days)
- `heatDD` (heating degree days)
- `revenue`
- `type` (`dt4training` or `dt4testing`)

**Note:** the CSV is not bundled in the notebook file itself — upload it to the Colab session (or mount from Drive) before running.

## Models Covered

| # | Model | Predictors |
|---|---|---|
| 1 | Simple Linear Regression | `production` |
| 2 | Multiple Regression | `production`, `heatDD` |
| 3 | Winter Dummy Variable | `production`, `winter` |
| 4 | Winter + Summer Dummy Variables | `production`, `winter`, `summer` |
| 5 | Winter × Production Interaction | `production`, `winter`, `winter_interaction` |

Each model is fit on `dt4training` and evaluated on `dt4testing` using mean absolute percentage error (MAPE), with matching visualizations (actual vs. predicted revenue, or trend lines by season).

## Notebook Structure

| Section | Content |
|---|---|
| 1. Setup | Imports, float display formatting |
| 2. Load and Inspect the Data | Read CSV, parse dates, check for missing values |
| 3. Visualizing Monthly Revenue | Revenue over time; heating vs. cooling split; revenue vs. production |
| 4. Correlation Analysis | Correlation matrix across revenue, production, coolDD, heatDD |
| 5. Training vs. Testing Data | Split into `train_df` / `test_df` |
| 6. Model 1: Simple Linear Regression | Fit, coefficients, test-set MAPE, actual-vs-predicted plot |
| 7. Model 2: Multiple Regression | Fit, coefficients, test-set MAPE, comparison plot, residual check |
| 8. Model 3: Winter Dummy Variable | Add season flags, fit, test-set MAPE, winter/non-winter trend lines |
| 9. Model 4: Winter + Summer Dummy Variables | Fit, three-way trend line plot |
| 10. Model 5: Winter × Production Interaction | Fit with interaction term, winter/non-winter trend lines |
| 11. Summary of Results | Computed MAPE comparison table + written takeaway |

## Dependencies

```python
numpy
pandas
seaborn
matplotlib
statsmodels
```

These are pre-installed in the standard Google Colab environment, so no manual installation should be required.

## How to Run

1. Open the notebook in Google Colab.
2. Upload `AICPA_regressionAnalysisData.csv` to the Colab session (or adjust the `pd.read_csv(...)` path if using Drive).
3. **Run all cells in order, top to bottom** (Runtime → Run all). The Section 11 summary table depends on variables (`mape_simple`, `mape_multi`, `mape_winter`) created earlier in the notebook — running out of order or restarting the runtime partway through will cause a `NameError` there.
4. Review each model's OLS summary, MAPE output, and plots, then check the Section 11 summary table for the side-by-side comparison.

## Reference Results

Based on a prior run of this modeling logic:

- Model 1 (Simple Linear Regression): MAPE ≈ 25.4%
- Model 2 (Multiple Regression): MAPE ≈ 13.9%
- Model 3 (Winter Dummy Variable): MAPE ≈ 15.9%

## Author

Eshaal Iqbal

---
*This README was generated from the cell code and markdown in `Hotazel_Steam_Regression_Modeling_cleaned.ipynb`.*
