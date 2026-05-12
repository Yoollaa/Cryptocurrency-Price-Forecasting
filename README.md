# Bitcoin Cryptocurrency Price Forecasting - MLP vs LSTM

## Project Overview

This project predicts the **next-day Bitcoin closing price** using the previous **30 days of historical closing prices**.

The project compares two models:

1. **Multi-Layer Perceptron (MLP)**
2. **Long Short-Term Memory Network (LSTM)**

The forecasting task is treated as a **supervised regression problem**, where the input is a 30-day lookback window and the output is the next-day Bitcoin closing price.

---

## Project Details

| Item | Description |
|---|---|
| Student Name | Marize Wassef |
| Project / Case Study | Case Study 2: Cryptocurrency Price Forecasting |
| Dataset | `Bitcoin_Daily.csv` |
| Method | MLP and LSTM using 30-day lookback windows |
| Target Variable | Next-day Bitcoin closing price |
| Date | 11 May 2026 |

---

## Dataset

The project uses the dataset file:

```text
Bitcoin_Daily.csv
```

The dataset contains daily Bitcoin market data.

| Column | Description |
|---|---|
| `timestamp` | Daily date |
| `open` | Opening price of Bitcoin |
| `high` | Highest price of the day |
| `low` | Lowest price of the day |
| `close` | Closing price of Bitcoin |
| `volume` | Daily traded volume |

### Dataset Summary

| Feature | Value |
|---|---|
| Number of rows | 1,674 |
| Number of columns | 6 |
| Date range | 2019-01-01 to 2023-08-01 |
| Missing values | 0 |

---

## Forecasting Task

The goal of this project is to forecast the next-day Bitcoin closing price.

```text
Input  : Previous 30 days of Bitcoin closing prices
Output : Next-day Bitcoin closing price
```

Because the target variable is a continuous numerical value, this is a **regression problem**.

---

## Methodology

### 1. Data Preprocessing

The `close` price column is selected as the main forecasting variable.

The closing prices are scaled between 0 and 1 using `MinMaxScaler`. Scaling helps neural networks train more efficiently because all values are placed within the same range.

### 2. Lookback Window Creation

A 30-day lookback window is created.

This means each model receives the previous 30 Bitcoin closing prices and tries to predict the closing price of the next day.

Example:

```text
Day 1 to Day 30  → Predict Day 31
Day 2 to Day 31  → Predict Day 32
Day 3 to Day 32  → Predict Day 33
```

### 3. Train/Test Split

The dataset is split chronologically:

```text
Training set : First 80%
Testing set  : Last 20%
```

A chronological split is used because this is a time-series forecasting problem. Random splitting is avoided because it could mix future data into the training process.

---

## Models Used

## 1. Multi-Layer Perceptron Model

The MLP model is a feedforward neural network.

It receives the 30-day price window as a flat input.

```text
MLP input shape: (samples, 30)
```

### MLP Architecture

```text
Input Layer: 30 neurons
Hidden Layer 1: 64 neurons + ReLU
Hidden Layer 2: 32 neurons + ReLU
Output Layer: 1 neuron
```

The output layer produces one predicted value: the next-day Bitcoin closing price.

---

## 2. Long Short-Term Memory Model

The LSTM model is a sequence-based deep learning model.

It receives the same 30-day price window, but keeps the order of the days.

```text
LSTM input shape: (samples, 30, 1)
```

LSTM is suitable for time-series forecasting because it can learn patterns from ordered data and remember useful information from previous time steps.

### LSTM Architecture

```text
Input size: 1
Hidden size: 64
Output layer: Linear layer with 1 output
```

---

## Training Setup

| Parameter | Value |
|---|---|
| Optimizer | Adam |
| Loss Function | Mean Squared Error Loss |
| Epochs | 10 |
| Learning Rate | 0.001 |
| Batch Size | 32 |
| Lookback Window | 30 days |
| Train/Test Split | 80% / 20% |

---

## Evaluation Metrics

The models are evaluated using three regression metrics:

| Metric | Meaning |
|---|---|
| MSE | Mean Squared Error. Penalizes larger errors strongly. |
| MAE | Mean Absolute Error. Shows the average prediction error in price units. |
| MAPE | Mean Absolute Percentage Error. Shows the average percentage error. |

---

## Results

| Model | MSE | MAE | MAPE (%) |
|---|---:|---:|---:|
| MLP | 1,648,744.25 | 1,013.33 | 4.53% |
| LSTM | 1,291,356.38 | 794.61 | 3.44% |

### Result Interpretation

In this run, the **LSTM model performed better** than the MLP model.

The LSTM achieved:

```text
Lower MSE
Lower MAE
Lower MAPE
```

This suggests that the LSTM was better at capturing time-dependent patterns in Bitcoin price movement.

However, cryptocurrency prices are highly volatile, so the model should not be used as guaranteed financial advice.

---

## Sample Prediction Output

| Date | Actual Close | MLP Prediction | LSTM Prediction |
|---|---:|---:|---:|
| 2022-09-07 | 19,292.84 | 20,021.64 | 19,745.14 |
| 2022-09-08 | 19,319.77 | 19,890.87 | 19,626.43 |
| 2022-09-09 | 21,360.11 | 19,864.45 | 19,525.88 |
| 2022-09-10 | 21,648.34 | 20,016.43 | 19,642.45 |
| 2022-09-11 | 21,826.87 | 20,155.97 | 19,868.14 |
| 2022-09-12 | 22,395.74 | 20,369.59 | 20,153.28 |
| 2022-09-13 | 20,173.57 | 20,745.85 | 20,505.57 |
| 2022-09-14 | 20,226.71 | 20,855.50 | 20,642.73 |
| 2022-09-15 | 19,701.88 | 21,167.08 | 20,689.81 |
| 2022-09-16 | 19,803.30 | 21,074.98 | 20,628.04 |

---

## Output Files

When the script is executed, it creates an `outputs` folder containing charts and CSV files.

```text
outputs/
├── close_trend.png
├── moving_averages.png
├── mlp_actual_vs_predicted.png
├── lstm_actual_vs_predicted.png
├── training_loss.png
├── metrics.csv
└── sample_predictions.csv
```

### Output File Description

| File | Description |
|---|---|
| `close_trend.png` | Shows the daily Bitcoin closing price trend. |
| `moving_averages.png` | Shows the closing price with 7-day and 30-day moving averages. |
| `mlp_actual_vs_predicted.png` | Compares actual prices with MLP predictions. |
| `lstm_actual_vs_predicted.png` | Compares actual prices with LSTM predictions. |
| `training_loss.png` | Compares MLP and LSTM training loss. |
| `metrics.csv` | Stores MSE, MAE, and MAPE results. |
| `sample_predictions.csv` | Stores sample actual and predicted prices. |

---

## Installation

Install the required Python libraries using the command below:

```bash
pip install pandas numpy matplotlib torch scikit-learn
```

---

## How to Run the Project

1. Download or clone this repository.
2. Place `Bitcoin_Daily.csv` in the same folder as the Python script.
3. Open Terminal, Command Prompt, VS Code Terminal, or Git Bash.
4. Run the Python file:

```bash
python ML and DL Techniques – Week 5 Final Project - Cryptocurrency Price Forecast.ipynb
```

After running the script, the console will display:

```text
Dataset information
Training loss per epoch
MLP evaluation results
LSTM evaluation results
Final model comparison
```

The script will also save charts and CSV files inside the `outputs` folder.

---

## Main Python File

The main Python file should be saved as:

```text
ML and DL Techniques – Week 5 Final Project - Cryptocurrency Price Forecast.ipynb
```

This file performs the full workflow:

```text
1. Import required libraries
2. Load the Bitcoin dataset
3. Convert timestamp to date format
4. Sort the dataset chronologically
5. Check missing values and summary statistics
6. Create moving averages
7. Scale closing prices
8. Create 30-day lookback windows
9. Split data into training and testing sets
10. Train the MLP model
11. Train the LSTM model
12. Evaluate both models
13. Save output charts
14. Save metrics and sample predictions
15. Print the final comparison
```

---

## Ethical Note

This project is created for educational purposes.

Cryptocurrency forecasting is uncertain because prices can be affected by many external factors, including:

```text
Investor sentiment
Regulation
Market liquidity
Macroeconomic news
Exchange activity
Speculation
Sudden market shocks
```

The model uses historical price patterns only and does not guarantee future performance or profit.

---

## Limitations

The main limitations of this project are:

1. The model uses only historical closing prices.
2. External variables such as news, sentiment, regulation, and macroeconomic indicators are not included.
3. Bitcoin prices are highly volatile and difficult to forecast accurately.
4. The models are relatively simple and can be improved further.
5. Results may vary slightly between different machines or training runs.

---

## Future Improvements

Possible improvements include:

1. Add more input features such as `open`, `high`, `low`, and `volume`.
2. Include technical indicators such as RSI, MACD, and Bollinger Bands.
3. Add sentiment analysis from news or social media.
4. Increase the number of epochs.
5. Tune hyperparameters such as hidden size, learning rate, and batch size.
6. Compare with additional models such as GRU, CNN-LSTM, Random Forest, or XGBoost.
7. Use walk-forward validation for more realistic time-series evaluation.

---

## Final Conclusion

This project successfully compares MLP and LSTM models for Bitcoin next-day closing price prediction.

The LSTM model achieved better performance in this run, with a lower MAPE of **3.44%** compared with the MLP MAPE of **4.53%**.

This supports the idea that sequence-aware deep learning models can be more effective for time-series forecasting tasks than simple feedforward models.

---

## Author

**Marize Wassef**

Machine Learning and Deep Learning Techniques  
Final Project - Cryptocurrency Price Forecasting
