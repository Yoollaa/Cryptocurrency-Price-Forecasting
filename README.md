# Bitcoin Cryptocurrency Price Forecasting - MLP vs LSTM

This repository contains a machine learning and deep learning project that predicts the next-day Bitcoin closing price using the previous 30 days of historical closing prices. The project compares a Multi-Layer Perceptron (MLP) with a Long Short-Term Memory (LSTM) neural network.

## Dataset

The project uses `Bitcoin_Daily.csv`, which contains daily Bitcoin market data with these columns:

- `timestamp`: daily date
- `open`: opening price
- `high`: highest price of the day
- `low`: lowest price of the day
- `close`: closing price and target variable
- `volume`: daily traded volume

Dataset period: 2019-01-01 to 2023-08-01. Total rows: 1674.

## Forecasting Task

Input: previous 30 days of Bitcoin closing prices.
Output: next-day Bitcoin closing price.

## Models

1. MLP - receives the 30-day window as flattened input with shape `(samples, 30)`.
2. LSTM - receives the same 30-day window as ordered sequence input with shape `(samples, 30, 1)`.

## Requirements

```bash
pip install pandas numpy matplotlib torch scikit-learn
```

## Repository Structure

```text
bitcoin-forecasting-project/
├── Bitcoin_Daily.csv
├── bitcoin_forecasting_solution_github.py
├── README.md
└── outputs/
    ├── close_trend.png
    ├── moving_averages.png
    ├── mlp_actual_vs_predicted.png
    ├── lstm_actual_vs_predicted.png
    ├── training_loss.png
    ├── metrics.csv
    └── sample_predictions.csv
```

## How to Run

Place `Bitcoin_Daily.csv` and `bitcoin_forecasting_solution_github.py` in the same folder. Then run:

```bash
python bitcoin_forecasting_solution_github.py
```

The script prints dataset information, training loss, MSE, MAE, and MAPE. It also saves charts and CSV files inside the `outputs` folder.

## Sample Results

| Model | MSE | MAE | MAPE (%) |
|---|---:|---:|---:|
| MLP | 1,648,744.25 | 1,013.33 | 4.53% |
| LSTM | 1,291,356.38 | 794.61 | 3.44% |

In this run, the LSTM achieved lower error than the MLP, suggesting that sequence-aware models can better capture temporal patterns in cryptocurrency price data. Results may vary slightly between machines.

## Ethical Note

This model is for educational purposes. Cryptocurrency forecasts are uncertain and should not be treated as guaranteed financial advice.

