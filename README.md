# StrataScrath

This repo contains a small ML workflow (in a Jupyter notebook) for **predicting delivery time** from historical order data.

## Project structure

- `code.ipynb`: end-to-end notebook (load data → feature engineering → train/evaluate models)
- `historical_data.csv`: dataset used by the notebook

## What `code.ipynb` does

- Loads `historical_data.csv`
- Cleans/imputes a few numeric fields and drops rows missing required columns
- Creates features such as:
  - hour of day, weekend flag
  - one-hot encodings for `market_id`, `store_primary_category`, `order_protocol`
  - target encoding for `store_id`
- Trains and compares:
  - `LinearRegression`
  - `RandomForestRegressor`
- Evaluates using **MAE** (mean absolute error) on a train/test split

## Setup (Windows / PowerShell)

From the repo root:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
pip install pandas scikit-learn category-encoders jupyter
```

## Run the notebook

The notebook expects the CSV at `prob1/historical_data.csv` and reads it via a relative path (`./historical_data.csv`), so run Jupyter from inside `prob1/`:

```powershell
cd prob1
jupyter notebook
```

Then open `code.ipynb` and run all cells.

## Notes

- **Target definition**: the notebook defines `interval` as the time difference between `actual_delivery_time` and `created_at` (in seconds).
- **Reproducibility**: the train/test split uses `random_state=42`.
- If you want to use `datasets.zip`, extract it into `datasets/` (or update paths in the notebook).

