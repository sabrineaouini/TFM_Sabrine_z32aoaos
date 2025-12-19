# Bitcoin Price Forecasting Using Technical Indicators and Time Series Models

This repository contains the code developed for a **Master’s thesis project** focused on **Bitcoin price forecasting** using a combination of technical indicators and macroeconomic variables.  
The study integrates **technical analysis methods** (moving averages, OBV, MACD...) with **advanced time series models**.

The main objective is to assess how complementary modeling approaches can be used to forecast highly volatile financial markets such as Bitcoin.

---

## 1. Background and Motivation

Bitcoin is a digital asset characterized by extreme volatility, influenced by supply and demand dynamics, regulatory decisions, and global macroeconomic and geopolitical uncertainty.  
Accurate **price forecasting** is therefore of significant interest for both investors and academic researchers.

**Long Short-Term Memory (LSTM)** networks were introduced to overcome the vanishing gradient problem in recurrent neural networks and to capture long-term temporal dependencies.  
The **Prophet** model, developed by Meta (Facebook), is an additive forecasting model designed to handle trend changes, seasonality, and external regressors in a robust and interpretable way.

---

## 2. Data Sources

The project relies on daily data from multiple sources:

- **Bitcoin price data (`bitcoin.csv`)**  
  OHLCV data (Open, High, Low, Close, Volume), typically obtained from financial platforms such as Yahoo Finance.

- **Gold Futures (`GC=F`)**  
  Retrieved using the Python library `yfinance`, capturing interactions between Bitcoin and traditional safe-haven assets.

- **Economic Policy Uncertainty Index (EPU)**  
  A news-based index measuring economic policy uncertainty derived from newspaper article frequency.

- **Geopolitical Risk Index (GPR / GPRD)**  
  Developed by Caldara and Iacoviello, this index quantifies global geopolitical tensions.

All time series are aligned to a daily frequency and **shifted by one day** to prevent information leakage.

---

## 3. Technical Indicators

The following technical indicators are computed using the Bitcoin closing price:

| Indicator | Description |
|---------|-------------|
| Pct_change | Daily return |
| MA | Simple Moving Average (30 days) |
| EMA | Exponential Moving Average |
| OBV | On-Balance Volume |
| MACD | Difference between EMA(12) and EMA(26) |
| Signal | EMA(9) of MACD |
| PSAR | Parabolic Stop and Reverse |

These indicators capture trend, momentum, and volume-based market dynamics.

---

## 4. Data Preprocessing

The preprocessing pipeline includes:

- Merging technical indicators with macroeconomic variables  
- Removing missing observations  
- Feature scaling (StandardScaler / RobustScaler)  
- Generating sliding time windows (`lookback`)  
- Time-aware split into **training (70%)** and **testing (30%)** sets  

The target variable is the **Bitcoin closing price**.

---

## 5. Modeling Approaches

### 5.1 LSTM Network

- Multivariate input sequences  
- Hyperparameter optimization using **Optuna**  
- Tuned parameters include:
  - number of LSTM layers
  - number of units
  - dropout rate
  - optimizer
  - learning rate
  - lookback window
- Evaluation metrics:
  - RMSE
  - MAE
  - R²

### 5.2 Prophet Model

- Additive time series model (trend + seasonality)
- Integration of **external regressors**
- Rolling-origin cross-validation
- Multi-horizon forecasting (H = 1, 5, 15 days)

### 5.3 Hybrid Model (Prophet + LSTM)

- Prophet models linear trend and seasonality
- LSTM learns the **residual component**
- Final prediction = Prophet forecast + LSTM residual prediction


### 5.4 Experimental Extension

- Exploratory use of a **Large Language Model (Gemini)** for text-based forecasting
- Strictly academic and comparative purpose

---

## 6. Cross-Asset Extension: Application to Ethereum

In addition to Bitcoin, the **same methodological pipeline** was systematically applied to **Ethereum (ETH)** in order to assess the **robustness, stability, and transferability** of the proposed forecasting approaches.

All preprocessing steps, feature engineering procedures, model architectures, hyperparameter optimization strategies, and evaluation protocols were kept **identical** across assets.  
This includes:

- Data collection and alignment at a daily frequency  
- Computation of technical indicators  
- Integration of macroeconomic and geopolitical variables  
- Time-aware train/test splitting  
- Model training, validation, and evaluation using identical metrics  

## 7. Installation and Execution

### Requirements
- Python = 3.12
- Jupyter Notebook (Colab)
- Git

### Installation
```bash
git clone <repository-url>
cd <project-directory>
pip install -r requirements.txt
