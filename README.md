# Simple-Two-Pairs-Trading-Strategies

Code 1: Multi-Pair Selection and ML-Based Pairs Trading
Purpose:
Identifies tradable stock pairs from a pool of S&P 50 and 50 DJIA-like candidates, using stats and machine learning (ML) to generate signals.
Great for practicing pair selection and ML—key quant skills in HK’s finance hub.
Strategy:
Pairs Selection: Combines 50 S&P stocks and 50 non-overlapping large-cap stocks (~4,950 pairs).
Statistical Metrics: Scores pairs using correlation, z-score of price spread, and cointegration p-value.
ML Signal Generation: Trains SVM and Random Forest to predict spread convergence (1) or divergence (0).
Execution: Signals trigger when z-score > 2 (entry) or < 0.5 (exit), aiming for mean reversion profits.
Logic:
Fetch price data (2010–2024) via yfinance.
Compute spread (ticker1/ticker2) and features:
Z-score: Spread deviation from rolling mean.
Correlation: Price co-movement strength.
Cointegration: Long-term relationship (p-value < 0.05 = tradable).
Pairing score = correlation × (1 - p-value) × |z-score|.
Train ML models on features, apply signals to top pairs.
Visualize top 20 pairs (heatmap, scatter, bar plots).
Limitations & Reminder:
Not Profitable in Real Life: No transaction costs, slippage, or risk controls; ML overfits historical data.
Naive Version: Assumes static relationships, ignores HK-specific markets (e.g., HSI).
Advice:
HK Twist: Swap S&P/DJIA for HSI stocks (e.g., 0700.HK for Tencent) using yfinance with .HK suffixes.*
ML Upgrade: Add volume or volatility features; use time-series splits to prevent overfitting.*
Tags:
#PairsTrading #MachineLearning #QuantResearch #StatisticalArbitrage #Python #DataScience #Finance
Code 2: Single-Pair Backtesting with Dual Strategy
Purpose:
Backtests a pairs trading strategy on one pair (e.g., AAPL-MSFT) with k-fold validation and performance metrics.
Ideal for learning backtesting and risk analysis—skills HK banks like HSBC value.
Strategy:
Pairs Trading: Exploits spread mean reversion for one pair.
Single Strategy: Long/short one stock vs. the other (z > ±1.5 entry, |z| < 0.75 exit).
Dual Strategy: Trades both stocks independently based on z-score thresholds.
Performance: Evaluates returns (gross/net), Sharpe/Calmar ratios, drawdowns.
Logic:
Fetch daily data (2000–2025) via yfinance, normalize prices.
Compute spread (ticker1 - hedge_ratio × ticker2) using OLS regression for hedge ratio.
Z-score triggers:
Single: Long ticker1/short ticker2 (z < -1.5), reverse (z > 1.5), exit (|z| < 0.75).
Dual: Separate long/short signals for each stock.
Backtest with costs (0.1% commission, 0.05% slippage) and 5-fold validation.
Visualize prices, signals, equity curve, and minute-level signals (last day).
Limitations & Reminder:
Not Profitable in Real Life: Fixed thresholds and hedge ratio miss market dynamics; costs kill profits.
Naive Version: No risk limits, U.S.-focused (AAPL-MSFT), not tuned for HK markets.
Advice:
HK Relevance: Test HK pairs (e.g., 0700.HK vs. 0005.HK [HSBC]); optimize thresholds with grid search.*
Realism Boost: Use rolling hedge ratios and cap drawdowns (e.g., 5% max loss).*
Tags:
#PairsTrading #Backtesting #Cointegration #QuantStrategy #Python #RiskManagement #Finance
