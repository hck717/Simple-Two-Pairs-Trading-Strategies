# Simple-Two-Pairs-Trading-Strategies

Code 1: Multi-Pair Selection and ML-Based Pairs Trading
Purpose:

This script identifies tradable stock pairs from a pool of S&P 50 and 50 DJIA-like candidates, using statistical and machine learning (ML) methods to generate trading signals.

Strategy:

Pairs Selection: Combines 50 S&P stocks and 50 non-overlapping large-cap stocks, then evaluates all possible pairs (~4,950 combinations) for tradability.
Statistical Metrics: Uses correlation, z-score of price spread, and cointegration (p-value) to score pairs.
ML Signal Generation: Trains SVM and Random Forest classifiers to predict if a spread will converge (1) or diverge (0), generating entry/exit signals when z-scores exceed thresholds (e.g., |z| > 2 for entry, |z| < 0.5 for exit).
Execution: Signals are based on ML consensus and z-score extremes, aiming to profit from mean reversion.
Logic:

Fetch historical price data (2010–2024) via yfinance.
Compute spread (ticker1/ticker2) and features:
Z-score: Measures spread deviation from its rolling mean.
Correlation: Assesses price co-movement.
Cointegration: Tests long-term statistical relationship (p-value < 0.05 = cointegrated).
Pairing score = correlation × (1 - p-value) × |z-score|—high scores indicate tradable pairs.
Train ML models on features to predict spread direction, then apply signals to top pairs.
Visualize results (heatmap, scatter, bar plots) for top 20 pairs.
Limitations & Reminder:

Not Profitable in Real Life: Ignores transaction costs, slippage, and market impact. ML models overfit historical data, and naive thresholds (z > 2) lack robustness.
Naive Version: Assumes constant relationships, no risk controls (e.g., stop-loss), and no HK-specific tuning (e.g., HSI stocks).
Advice:

Adapt for HK: Replace S&P/DJIA with HSI constituents (e.g., 0700.HK for Tencent). Use HKEX data via yfinance (e.g., '0700.HK').*
Improve ML: Add features (e.g., volatility, volume) and use time-series cross-validation to avoid overfitting.*
Tags: #PairsTrading #MachineLearning #QuantResearch #StatisticalArbitrage #Python #DataScience #Finance

Code 2: Single-Pair Backtesting with Dual Strategy
Purpose:

This script backtests a pairs trading strategy on a single user-defined pair (e.g., AAPL-MSFT), evaluating performance with k-fold cross-validation and detailed metrics.

Strategy:

Pairs Trading: Trades one pair based on spread mean reversion.
Single Strategy: Long/short one stock vs. the other when z-score exceeds ±1.5, exits at ±0.75.
Dual Strategy: Independently trades both stocks (long/short ticker1, long/short ticker2) based on the same z-score thresholds.
Performance: Assesses returns (gross/net), Sharpe/Calmar ratios, and drawdowns, with/without transaction costs.
Logic:

Fetch daily data (2000–2025) via yfinance, normalize prices, and compute spread (ticker1 - hedge_ratio × ticker2).
Hedge ratio from OLS regression ensures spread stationarity.
Z-score of spread triggers signals:
Single: Long ticker1/short ticker2 (z < -1.5), reverse (z > 1.5), exit (|z| < 0.75).
Dual: Separate signals for each stock based on z-score.
Backtest with costs (0.1% commission, 0.05% slippage) and k-fold validation (5 folds).
Visualize normalized prices, signals, equity curve, and minute-level signals for the last day.
Limitations & Reminder:

Not Profitable in Real Life: Static thresholds (1.5, 0.75) and fixed hedge ratio ignore dynamic market conditions. Costs erode profits, and no risk management (e.g., position sizing) is included.
Naive Version: Assumes perfect execution, no latency, and U.S.-centric (AAPL-MSFT) without HK relevance.
Advice:

HK Focus: Test HK pairs (e.g., 0700.HK vs. 0005.HK [HSBC]) and adjust thresholds via optimization (e.g., grid search).*
Enhance Realism: Add dynamic hedge ratios (rolling OLS) and risk limits (e.g., max 5% drawdown).*
Tags: #PairsTrading #Backtesting #Cointegration #QuantStrategy #Python #RiskManagement #Finance

General Comments & Preparation Tie-In
Why Useful for You: Both scripts align with Junior Quant Analyst skills—data handling (Pandas), modeling (statsmodels), ML (Scikit-learn), and finance (pairs trading). They’re portfolio-worthy for HK recruiters (e.g., HSBC, HKEX).
Next Steps:
Modify Code 1 to screen HSI pairs and Code 2 to backtest them.
Add to your GitHub (as in my prior plan) with READMEs explaining logic and HK context.
Study “Quantitative Trading” by Ernest Chan (HKU library) for pairs trading theory.
Real-World Caution: These are educational toys—real quant roles at HK hedge funds (e.g., Citadel) demand more complexity (e.g., high-frequency data, robust risk models).
Let me know if you want help adapting these for HSI stocks or refining them further!
