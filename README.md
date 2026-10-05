# Freight Rate Prediction

Machine Learning Engineer assessment for predicting freight load rates.

## Approach

The labeled dataset was explored and cleaned before training.

Main preprocessing steps:
- Converted negative weight values to their absolute values.
- Handled missing numerical values using median imputation.
- Converted the date column to datetime.
- Created month, day of week, and day of year features.
- One-hot encoded categorical features.

Because the data is time-based, I used a chronological validation split instead of a random split. January through September 2025 was used for training and October 2025 was used for validation.

A median baseline model was compared with Linear Regression.

Validation results:

| Model | MAE | RMSE |
|---|---:|---:|
| Baseline | 1146.79 | 1567.97 |
| Linear Regression | 140.66 | 651.94 |

Linear Regression was selected as the final model. I also used expanding-window backtesting across July, August, September, and October.

Average backtest results:
- MAE: 184.61
- RMSE: 640.57

The final model was trained on all 48,000 labeled rows before generating the final validation predictions.

## Project Structure

- `freight_rate_prediction.ipynb` - complete analysis, training, validation, and prediction workflow
- `data/` - assessment input files
- `validation_predictions.csv` - final predictions for the 12,000 validation loads
- `score.py` - provided validation script
- `requirements.txt` - Python dependencies
- `scorer_results/candidate_december.png` - December prediction chart

## Run

Install the dependencies:

```bash
python -m pip install -r requirements.txt
```

Run the notebook:

```bash
jupyter notebook freight_rate_prediction.ipynb
```

After generating the prediction files, run the provided scorer:

```bash
python score.py --predictions validation_predictions.csv --december-predictions data/december-chart-inputs.csv
```

The scorer validates the prediction files and creates:

```text
scorer_results/candidate_december.png
```