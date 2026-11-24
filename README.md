# AO vs GWO for XGBoost Hyperparameter Optimization on LQ45 Stocks

Code for the paper "Hyperparameter Optimization of XGBoost Using the Aquila
Optimizer and Grey Wolf Optimizer for Closing Price Prediction of LQ45 Stocks".

## Overview
This study compares the Aquila Optimizer (AO) and the Grey Wolf Optimizer (GWO)
for tuning eight XGBoost hyperparameters (n_estimators, learning_rate, max_depth,
subsample, colsample_bytree, gamma, reg_alpha, reg_lambda) to predict the
next-day closing price, Close(t+1), of 37 LQ45 stocks from 2021 to 2025.
The fitness function is the validation MAPE. Models are evaluated on a held-out
test set with MAPE, RMSE, MAE, and R².

## Experimental setup
- Data: daily OHLCV from Yahoo Finance (Jan 4, 2021 – Dec 30, 2025), 37 stocks
- Features: OHLCV at day t, lags 1–2, and temporal features
  (day of week, day of month, month, year)
- Split: chronological 70% / 15% / 15% (train / validation / test)
- Optimizers: population size 10, up to 200 iterations, patience 50
- Runs: 10 seeds (1–10) per stock and optimizer, 740 runs in total
- Model selection: run with the lowest validation MAPE
- Statistical tests: Wilcoxon signed-rank, Diebold–Mariano, Mann–Whitney U
  (Holm-corrected), bootstrap confidence interval, Spearman correlation

## Repository contents
- `<source codek>.ipynb`: the complete pipeline in one notebook (data download,
  feature engineering, AO and GWO implementation, 740 optimization runs,
  evaluation, and statistical tests)

## How to run
1. Install the packages listed below.
2. Open the notebook and run all cells in order.
   Price data are downloaded with `yfinance` (Jan 4, 2021 – Dec 30, 2025),
   so no data files are included.
3. The full experiment (740 runs) is computationally heavy. Intermediate results
   are saved as checkpoints, so an interrupted run can be resumed.

## Reproducibility
Python 3.13.7, xgboost 3.2.0, scikit-learn 1.9.0, NumPy 2.2.6, pandas 3.0.3,
SciPy 1.17.1, statsmodels 0.15.0, yfinance 1.7.0.
Random seeds are fixed (optimizer seeds 1–10, XGBoost random_state = 42).

## Citation
To be added after publication.
