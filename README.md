## Project Tetra: Sniper Stock Prediction
By: Danny Whitaker

**Goal:** The goal of Tetra was to create a machine learning pipeline to predict 5-day directional price movements for the S&P 500 and other stocks with at least 55% accuracy. This gives the pipeline a statstical edge over flipping a coin or guessing on price movements.

**Overall Results:** The final results of the implemeneted Sniper strategy was that it achieved roughly ~60% accuracy on major market indicies like the S&P 500 or QQQ. This was down over a 12-year backtest from 2013-2025.

**Insights:** By filtering for high-confidence setups (setups that have > 60% probability) rather than trading every day and trying to learn from each trade, the model was successfully able to seperate market signal and noise allowing for it to achieve higher accuracy.

The primary predictive drivers were identified as **Volatility** and **Trend Structure** which are represented as 'atr_norm' and 'ema_ratio'.

# Project Overview
In todays world, financial markets are noisy, and non-static environments were often times simple models fail or achieve low accuracy. 

Instead of creating another model similar to one that I just described, I opted to try to create a model that implements a confidence threshold mechanism. The model acts as a sniper trader, and reamins on the sidelines during choppy price movements and conditions. The model as a sniper only executed trades when the predicted probability of success is statistically great.

# Stack
**Analysis Tools:** Python, Pandas, Numpy, YFinance
**Machine Learning:** Scikit-Learn (Pipeline, StandardScaler), XGBoost, Random Forest, VotingClassifier
**Feature Eng:** TA-Lib (Technical Analysis)
**Visualizations:** Matplotlib, Seaborn

Prototype only:
**Deployment:** Streamlit (Interactive Dashboard experience


# Project Evolution
This project was designed to follow an iterative CRISP-DM approach to modeling:

**Phase 1: Baseline**
**Aproach:** Single XGBoost model that used raw technical indicators such as RSI and MACD.
**Results:** ~52% accuracy on major indicies but struggled with noise from the indiviudal stocks.
**What did I learn?:** Raw indicators alone; or indicators in general werent enough to make the model be able to predict the market. It needed context...

**Phase 2: Feature Engineering**
**Approach:** I introduced 'Lagged Features' (looking back 5 days) and 'Market Context' (merging SPY trends with individual stock ticker data).
**Result:** ~55% accuracy. The performance overall improved significantly, but the model still traded during high-risk, low-volatility periods which caused it to make foolish errors.
**What did I learn?:** I needed to find a way to filter out low-quality trade setups that it predicted.

**Phase 3: The Final "Sniper" Trader Strategy**
**Approach:** Implement an ensemble model that used votingclassifier and combined XGBoost with random forest to reduce overall variance. Then, wrap the created workflow in a pipeline to create reproducibility.

Lastly, apply the confidence threshold so that the only trades that are done are contingent on if the model's probability of success is > 60%.
**Result:** ~60% accuracy on indicies. The system made a tremendous increase in accuracy here as I know that anything beyond 55% is really hard to get. Our system that we created above successfully filtered out choppy price actions, which resulted in trading less frequently but with much higher precision.

# Usage Guide
1. Installation
Clone the repository and install the required dependencies above ^

2. Run
Configure tickers and run all cells

