# FTSE100-Trading-Strategy  

---

## 📌 Introduction
This project implements algorithmic trading strategies on the **FTSE 100 Index**, focusing on technical indicators such as **Relative Strength Index (RSI)**, **Moving Average Convergence Divergence (MACD)**, and a **Blended Strategy** that integrates multiple signals.  
The aim is to test whether combining momentum and trend indicators can outperform standalone approaches and a traditional **Buy-and-Hold** strategy in terms of risk-adjusted returns.  

The project evaluates the strategies based on standard performance metrics (cumulative returns, Sharpe ratio, alpha, beta, and maximum drawdown). The motivation is to assess how technical indicators and blended logic can provide traders and asset managers with consistent performance across changing market conditions.  

---

## 📊 Dataset
- **Index:** FTSE 100 (Financial Times Stock Exchange 100)  
- **Constituents:** 100 equities across multiple sectors (energy, finance, consumer staples, etc.)  
- **Data Source:** Yahoo Finance API (`yfinance` library)  
- **Data Frequency:** Daily OHLCV (Open, High, Low, Close, Volume)  
- **Period Covered:** July 2020 – July 2025 (5 years)  
- **Preprocessing Steps:**  
  - Forward-filled missing values where possible.  
  - Adjusted for stock splits and dividends.  
  - Survivorship bias minimized by including only securities consistently listed during the sample period.  
  - Ensured uniform coverage across all FTSE sectors to avoid pre-selection bias.  

This dataset captures multiple market phases (bull, bear, and transitional), providing a robust foundation for testing the resilience of trading strategies.  

---

## ⚙️ Methodology
The methodology follows a **quantitative, simulation-based approach** implemented in Python.  

### 1. Technical Indicators
- **RSI (Relative Strength Index):**  
  - 10-day window.  
  - Buy signal when RSI < 30, sell when RSI > 70.  

- **MACD (Moving Average Convergence Divergence):**  
  - Fast EMA = 8, Slow EMA = 17, Signal line = 9.  
  - Buy when MACD line crosses above signal; sell when it crosses below.  

- **Moving Average (MA):**  
  - 30-day SMA filter used for trend confirmation.  

### 2. Blended Strategy Logic
- Composite weighted scoring system:  
  - RSI → 40%  
  - MACD → 30%  
  - MA → 30%  
- Position entered only when multiple signals align.  
- Signals recalculated daily and rebalanced at close.  
- Designed to reduce false positives and increase robustness.  

### 3. Backtesting Framework
- **Portfolio Construction:** Equal-weight allocation to top signals (max 10 tickers).  
- **Performance Evaluation Metrics:**  
  - Cumulative Returns  
  - Sharpe Ratio  
  - Alpha & Beta (via CAPM regression)  
  - Maximum Drawdown  
  - Win Rate & Turnover  
- **Assumptions:**  
  - No transaction costs or slippage in baseline tests.  
  - Daily rebalancing.  
  - Minimum holding period enforced to avoid overfitting.  

---

## 📈 Results
The strategies produced distinct performance profiles over the 5-year period:  

- **RSI Only:**  
  - Cumulative return ≈ 56%  
  - Sharpe ratio ≈ 0.53  
  - Moderate drawdown (≈ –17%)  
  - Low win rate (~17%)  

- **MACD Only:**  
  - Cumulative return ≈ 78%  
  - Sharpe ratio ≈ 0.63  
  - High drawdown (≈ –43%)  
  - Better momentum capture but unstable in sideways markets  

- **Blended Strategy (RSI + MACD + MA):**  
  - Cumulative return ≈ **88%**  
  - Sharpe ratio ≈ **0.88**  
  - Drawdown ≈ –16%  
  - Win rate ≈ **52%**  
  - Balanced performance across sectors, with improved robustness  

- **Benchmark (Buy-and-Hold):**  
  - High returns in specific tickers (e.g., Rolls Royce, BAE Systems)  
  - Lacked risk-adjusted stability compared to blended strategy  
  - Exposed to deeper drawdowns in volatile phases  

📌 Conclusion: The **Blended Strategy** consistently outperformed standalone indicators and Buy-and-Hold in risk-adjusted terms, making it the most effective and scalable approach among those tested.  

---
