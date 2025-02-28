# Simple-Two-Pairs-Trading-Strategies


Project Overview

Pair-Trading-Using-Machine-Learning
📈 Exploring Pair Trading with Machine Learning: A Data-Driven Approach

I’m excited to share insights from my recent project where I developed two scripts for pair trading. One script screens multiple stock pairs using machine learning, while the other backtests a single pair with dual strategies. This project combines my data science skills with quantitative finance, inspired by Hong Kong’s financial ecosystem, particularly HSI volatility. I completed this work with the assistance of Grok 3 and various online resources. Here’s a breakdown of the process:

1. Data Science Workflow
The project involved several critical steps:

Data Collection: Utilized the yfinance API to gather stock prices for S&P 50 and large-cap DJIA-like stocks from 2010 to 2024, as well as minute-level data for a single pair from 2000 to February 2025.

Data Preprocessing: Cleaned the data by computing spreads, handling missing values, normalizing prices, and calculating z-scores.


2. Key Features for Trading

I selected the following features to enhance the model's predictive capabilities:

Z-score: Measures spread deviation from the 20-day rolling mean, indicating overbought or oversold conditions.

Correlation: Rolling 20-day correlation to assess the co-movement of stock pairs.

Cointegration: Engle-Granger test p-value to find long-term relationships between pairs.

Pairing Score: Combines correlation, p-value, and z-score to rank tradable pairs.

Normalized Spread: Calculates the difference between normalized prices to target mean reversion.


3. Model Evaluation Metrics

To assess the models' performance, I employed several metrics:

SVM Accuracy: Achieved around 70–80% accuracy, with a risk of overfitting.

Random Forest Accuracy: Performed slightly better, reaching 75–85% accuracy.

Annualized Return (Net): Estimated returns of approximately 5–10% from backtesting AAPL-MSFT.

Sharpe Ratio: Ranged from 1.5 to 2.0, indicating good risk-adjusted returns.

Max Drawdown: Reported a maximum drawdown of -15%, highlighting potential risk exposure.


4. Tech Stack

The project utilized a robust tech stack:

Programming Language:

Python 3.9

Libraries:

pandas, numpy for data manipulation, matplotlib, seaborn for visualization, scikit-learn for machine learning and model evaluation, statsmodels for statistical analysis, yfinance for accessing stock data


5. Results and Visualization

The models' predictions were visualized through various plots, showcasing trends in economic indicators, predicted trading signals, and feature importance. Key findings included:

Backtest Performance: Analyzed from 2010 to 2024, validating the models’ robustness.

I undertook this project to leverage my machine learning knowledge in real-world trading scenarios. While the predictions may not be perfect and there are areas for improvement, I am 

committed to continuing my journey by working on various projects to enhance my hands-on experience with ML and data.

