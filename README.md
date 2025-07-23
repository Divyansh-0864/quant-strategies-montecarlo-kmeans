# 📈 Quantitative Trading Strategies: Moving Average Crossover & Machine Learning Portfolio Optimization

This repository contains two end-to-end trading strategies implemented in Python using `yfinance`, `pandas`, and other scientific libraries.

---

## 🧠 Strategy 1: Moving Average Crossover + Monte Carlo Portfolio Optimization

### 🔹 A. Moving Average Crossover Backtest

A simple technical analysis strategy that simulates buying and selling a stock (default: AAPL) based on SMA crossovers.

- **Buy Signal**: When 5-day SMA > 20-day SMA
- **Sell Signal**: When 5-day SMA < 20-day SMA
- **Capital**: `₹10,000` initial
- **Output**:
  - Trade log
  - Final portfolio value

> 📊 **Backtest Output (Example)**  
> Final Portfolio Value: `₹9656.65` (based on data availability)

---

### 🔹 B. Monte Carlo Portfolio Simulation & Optimization (NSE Stocks)

A portfolio of 10 NSE large-cap stocks is simulated across 10,000 portfolios to identify the best asset allocation using Sharpe Ratio and volatility metrics.

- **Time Period**: Jan 2020 – Feb 2025
- **Investment**: ₹10,00,000
- **Optimization Objective**: 
  - Maximize Sharpe Ratio
  - Minimize Volatility
- **Output**: Efficient Frontier plot, weights, performance metrics

#### 🏆 Max Sharpe Portfolio
- **Final Value**: ₹28,69,248.54  
- **Cumulative Return**: 186.92%  
- **Annual Volatility**: 21.0%  
- **Sharpe Ratio**: 1.094  
- **Max Drawdown**: -36.2%  

#### 📉 Min Volatility Portfolio
- **Final Value**: ₹19,64,820.17  
- **Cumulative Return**: 96.48%  
- **Annual Volatility**: 17.4%  
- **Sharpe Ratio**: 0.852  

---

## 🤖 Strategy 2: Unsupervised Learning Portfolio with K-Means & Efficient Frontier

This advanced strategy uses **machine learning** to cluster stocks each month based on technical and fundamental features, and then builds optimized portfolios.

### 🔬 Workflow Summary

1. **Data Collection**:  
   - Fetch historical data for NIFTY 100 stocks from Yahoo Finance  
   - Calculate indicators: RSI, Bollinger Bands, ATR, MACD, Garman-Klass Volatility

2. **Feature Engineering**:  
   - Monthly aggregation  
   - Rolling returns (1M, 2M, 3M, 6M, 9M, 12M)  
   - Dollar volume filtering (top 50 stocks/month)  
   - Fama-French 5-factor betas via rolling regressions

3. **Clustering**:  
   - K-Means clustering using hand-crafted RSI-based centroids  
   - Select high-momentum cluster (e.g., Cluster 3: RSI ~ 70)

4. **Portfolio Optimization**:
   - For each month, use 1 year of historical prices
   - Use `PyPortfolioOpt` to find weights maximizing Sharpe Ratio
   - Apply constraints: max 10% per stock, min 0.5 × equal-weight

5. **Evaluation**:
   - Backtest monthly portfolio returns
   - Compare to NIFTY 100 benchmark (e.g., NETFNIF100.NS ETF)

---

### 📈 Performance Metrics

| Metric                   | Value         |
|--------------------------|---------------|
| **Cumulative Return**    | 63.38%        |
| **Annualized Return**    | 12.46%        |
| **Annualized Volatility**| 16.67%        |
| **Sharpe Ratio**         | 0.747         |
| **Max Drawdown**         | -23.41%       |

---

## 🛠️ Setup Instructions

### ✅ Requirements

```bash
pip install yfinance pandas numpy matplotlib scipy scikit-learn statsmodels pandas-ta pypfopt
```

---

## 🚀 Running the Code

### Strategy 1

- File: `moving_average_montecarlo.py`
- Run:

```bash
python moving_average_montecarlo.py
```

### Strategy 2

- File: `ml_clustering_portfolio.py`
- Run:

```bash
python ml_clustering_portfolio.py
```

---

## 📘 Notes

- **Data Source**: Yahoo Finance (via `yfinance`)
- **Benchmarks**: NIFTY 50 (`^NSEI`) and NIFTY 100 ETF (`NETFNIF100.NS`)
- **Factor Model**: Fama-French 5-Factor Model via `pandas-datareader`
- **Optimization**: Sharpe-maximization using `PyPortfolioOpt`

---

## 📊 Metrics Explained

| Metric         | Description                                                  |
|----------------|--------------------------------------------------------------|
| Cumulative Return | Total portfolio return over the period                     |
| Volatility     | Standard deviation of returns (annualized)                   |
| Sharpe Ratio   | Return per unit of risk (assumes risk-free rate ≈ 0)         |
| Max Drawdown   | Largest observed portfolio drop from peak to trough          |

---

## ⚠️ Limitations

While both strategies demonstrate powerful concepts in quantitative finance, they also come with several important limitations:

### 📉 Strategy 1: Moving Average & Monte Carlo Portfolio Optimization

- **Simplistic Trading Logic**: The moving average crossover strategy is a basic rule-based system and does not consider risk-adjusted position sizing, stop-loss, or transaction costs.
- **No Slippage or Fees**: Backtesting logic assumes ideal market conditions — no bid-ask spread, slippage, or commissions, which are unrealistic in live markets.
- **Fixed Parameters**: Short and long window sizes (5 & 20) are hardcoded and not optimized, which may lead to overfitting or poor generalization.
- **Monte Carlo is Allocation-Only**: The Monte Carlo simulation tests thousands of random portfolios but does not simulate trade sequences or time-based portfolio rebalancing.
- **Historical Bias**: The assumption that past returns and volatility will remain consistent in the future may not hold true in dynamic markets.

### 🤖 Strategy 2: Unsupervised Learning with K-Means & Factor Modeling

- **No Execution-Level Backtesting**: The strategy builds monthly portfolios but does not simulate individual trades, execution delays, liquidity constraints, or transaction costs.
- **Cluster Interpretability**: K-Means clustering uses features like RSI and MACD but doesn't provide economic rationale for why one cluster outperforms — it's a statistical black-box.
- **Data Lookahead Bias Risk**: Care must be taken to avoid using future information inadvertently (e.g., calculating returns or factors with future data).
- **Portfolio Drift Ignored**: Portfolios are constructed and assumed to hold throughout the month without mid-period adjustments, which ignores drift and market shocks.
- **Benchmark Comparison Limited**: The strategy compares performance visually to an index but lacks statistical significance testing or rolling performance metrics.

---


## ⚠️ Disclaimer

This repository is for **educational purposes only** and should not be considered financial advice or a recommendation to buy/sell any financial asset.

---

## 🙌 Contributions

Feel free to fork, contribute, or raise issues to improve the strategies.

---
