# Simple-Two-Pairs-Trading-Strategies

Project Overview
I created two scripts to dive into pair trading: one screens multiple stock pairs using machine learning, and the other backtests a single pair with dual strategies. This project bridges my data science expertise with quantitative finance, inspired by HK’s financial ecosystem (e.g., HSI volatility).

Script 1: Multi-Pair Selection with ML
Screens S&P 50 and 50 DJIA-like stocks to find tradable pairs, using statistical methods and machine learning for signals.

Script 2: Single-Pair Backtesting
Backtests a user-defined pair (e.g., AAPL-MSFT) with single and dual trading strategies.

Support
Grok 3 assisted with coding logic (e.g., ML tuning, backtesting loops).
Referenced Quantopian tutorials, Stack Overflow, and HKEX data guides.

Data Science Workflow
Data Collection

Source: yfinance API for stock prices.
Script 1: S&P 50 + 50 large-cap stocks (2010–2024).
Script 2: Single pair (e.g., AAPL-MSFT) from 2000–Feb 2025.
Fetched daily adjusted close prices; Script 2 also pulls minute-level data for recent days.
Data Preprocessing
Script 1: Computed ticker1/ticker2 spread, handled NaNs with dropna(), aligned dates.
Script 2: Normalized prices (price/price[0]), calculated spread with OLS hedge ratio, added z-scores.
Challenges: Adjusted for U.S. time zones (Script 2) and ensured data completeness.
Key Features for Trading
Script 1 (Multi-Pair)
Z-score: Spread deviation from 20-day rolling mean/std—signals overbought/oversold conditions.
Correlation: Rolling 20-day correlation—measures co-movement.
Cointegration: Engle-Granger test p-value—assesses long-term relationship.
Pairing Score: 
correlation
×
(
1
−
p-value
)
×
∣
z-score
∣
correlation×(1−p-value)×∣z-score∣—ranks tradability.
Script 2 (Single-Pair)
Normalized Spread: 
ticker1_norm
−
hedge_ratio
×
ticker2_norm
ticker1_norm−hedge_ratio×ticker2_norm—mean-reverting target.
Z-score: Standardized spread—drives entry/exit signals.
Hedge Ratio: OLS regression coefficient—balances pair positions.
Logic
Multi-Pair: Features feed ML models to predict spread direction.
Single-Pair: Z-score thresholds (e.g., ±1.5 entry, ±0.75 exit) trigger trades.
Model/Strategy Development
Script 1
Approach: SVM (RBF kernel, C=1.0) and Random Forest (100 trees) classify spread convergence/divergence.
Signals: Entry (|z| > 2) and exit (|z| < 0.5) when ML models agree.
Training: 80/20 train-test split on feature-label pairs.
Script 2
Single Strategy: Long/short pair based on z-score (e.g., long AAPL, short MSFT if z < -1.5).
Dual Strategy: Independent long/short signals for each stock.
Backtesting: 5-fold time-series cross-validation; includes 0.1% commission, 0.05% slippage.
Model Evaluation Metrics
Script 1
SVM Accuracy: ~70–80% (varies by run)—decent but overfitting risk.
Random Forest Accuracy: ~75–85%—slightly better feature handling.
Pairing Score: Top pairs (e.g., AAPL-NVDA) scored > 0.8—promising candidates.
Script 2
Annualized Return (Net): ~5–10% (AAPL-MSFT, varies by fold)—optimistic backtest.
Sharpe Ratio: 1.5–2.0 (net)—good but ignores real-world noise.
Max Drawdown: -15%—highlights risk exposure.
Caveat: Overly rosy metrics—lacks out-of-sample testing.
Tech Stack
Programming Language: Python 3.9—my go-to for quant projects.
Libraries:
pandas, numpy: Data wrangling and math.
matplotlib, seaborn: Plotting spreads, signals, equity curves.
scikit-learn: ML models and evaluation (SVM, RF, GridSearchCV).
statsmodels: Cointegration and OLS regression.
yfinance: Stock data fetching.
Results and Visualization
Script 1
Outputs: Ranked pair list (e.g., top 20 by pairing score).
Plots: Heatmap of features, scatter of z-score vs. correlation, bar chart of top pairs.
Findings: Pairs like MSFT-GOOGL showed high cointegration—potential trades.
Script 2
Outputs: Cumulative returns (gross/net), drawdowns, minute-level signals.
Plots: Normalized prices, z-score with signals, equity curve.
Findings: AAPL-MSFT showed mean reversion, but costs ate into profits.
