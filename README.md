# House Data Cleaning – First Pass

A step-by-step cleaning notebook for a messy house-sales dataset (1,200 rows, 36 columns). The goal is a dataset with no missing values, correct dtypes and no duplicates.

## Files

| File | Description |
|---|---|
| `clean_1.ipynb` | Cleaning notebook (executed, with outputs) |
| `train_0.csv` | Raw messy house data (1,200 rows, 36 columns) |

## What the notebook does

1. **Load & inspect** – `head`, `info`, check for duplicate rows and duplicate `Id`s (none found).
2. **Handle missing values**

| Column(s) | Missing | Fix |
|---|---|---|
| `LotFrontage` | 46 | Median |
| `MasVnrArea` | 35 | `0` (no masonry veneer) |
| `PoolQC` / `Alley` / `Fence` | 1,191 / 1,098 / 937 | `"None"` |
| `GarageType` | 56 | `"No Space"` |
| `GarageYrBlt` | 56 | `0` |
| `SaleType`, `HouseStyle` | 0 | Mode fill kept as a safeguard |

3. **Fix dtypes** – `SaleDate` → datetime, `GarageYrBlt` → nullable `Int64`.
4. **Verify** – `df.isnull().sum().sum() == 0`, final shape `(1200, 36)`.

## Tech stack

Python 3 · pandas · NumPy · Jupyter

## Run it

```bash
git clone https://github.com/Nirmalya625/data_cleaning-and-eda-for-data-analysis.git
cd data_cleaning-and-eda-for-data-analysis
pip install pandas numpy jupyter
jupyter notebook clean_1.ipynb
```

The notebook reads `train.0.csv`; the file in this repo is `train_0.csv`. Update the `pd.read_csv(...)` path or rename the file before running.

## Known limitations

- Median imputation is computed on the full dataset, so it is not leakage-safe for modelling.
- `GarageYrBlt = 0` is a placeholder, not a real year; a flag column or `NaN` would be safer.
- No EDA, outlier handling or feature engineering in this pass.

## Author

**Nirmalya** – [GitHub](https://github.com/Nirmalya625)
