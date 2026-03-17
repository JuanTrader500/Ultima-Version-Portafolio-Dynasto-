# Portafolio-De-Experts-Advisors-MT5

Algorithmic Trading Portfolio: Quantitative Assessment Report

Date: October 2026

Subject: Multi-Strategy Portfolio Performance & Robustness Analysis

Data Source: 5-Year MetaTrader Backtest Exports(2021-2025)

Methodology: Python (Pandas, Plotly, NumPy)

1. Executive Summary

The objective of this analysis was to evaluate the combined performance, risk profile, and statistical robustness of a diversified algorithmic trading portfolio. The portfolio consists of five distinct strategies applied across varying asset classes, including Indices (DAX40, US500), Commodities (Gold), and Forex (USDJPY).

The analysis successfully consolidated disjointed backtest data into a unified simulation model. Key findings indicate that combining these strategies into a single account potentially smooths the equity curve and diversifies risk, subject to the correlation findings detailed in Section 5.

2. Data Acquisition & Engineering

2.1. The Challenge: Unstructured Data

The raw data provided consisted of Strategy Tester Reports from MetaTrader 5. These files presented significant engineering challenges:

Format Issues: Files were nominally .xlsx or .csv but encoded in UTF-16 with non-standard delimiters.

Data Types: Financial values contained whitespace (e.g., 1 200.00), causing them to be interpreted as strings rather than floats.

2.2. The Solution: Custom Parsing Pipeline

We implemented a robust Python script using pandas to sanitize the data:

Dynamic Header Detection: The algorithm scans the file stream for the anchor string "Open Time" or "Hora de apertura" to identify the true start of the dataset.

Encoding Normalization: Automatic conversion from UTF-16 to UTF-8.

Type Casting: A rigorous cleaning function removed whitespace and converted string objects into floating-point numbers for mathematical operations.

3. Portfolio Simulation Methodology

To simulate a realistic trading environment, we moved beyond simple summation and implemented a Chronological Event-Driven Model.

Initial Capital: Fixed at $10,000 USD.

Trade Reconstruction: We calculated the net profit/loss per trade by differentiating the cumulative balance series (df.diff()).

Unified Timeline: All trades from the five strategies were merged into a single DataFrame and sorted by timestamp. This allowed us to visualize the portfolio's behavior as if all algorithms were running simultaneously on a single account.

3.1. Performance Metrics

We evaluated the portfolio using:

Cumulative Return (%): Total growth relative to the initial capital.

Max Drawdown (%): The largest peak-to-valley decline in the portfolio's equity, representing the maximum historical risk.

4. Robustness Testing: Monte Carlo Simulation

To validate that the portfolio's performance was not merely a result of "lucky timing" or a specific market sequence, we performed a Monte Carlo Simulation.

4.1. Methodology

Iterations: 100 unique simulations.

Process: The sequence of valid trades (Profit/Loss) was shuffled randomly using numpy.random.permutation.

Goal: To determine the distribution of possible outcomes and, most importantly, the Worst Case Scenario (WCS) drawdown.

4.2. Interpretation of Results

The "Cloud": The 100 simulations create a probability cloud.

Stability: If the real equity curve falls within the dense part of the cloud, the strategy is statistically normal.

Risk Assessment: We compared the Real Max Drawdown against the Monte Carlo Worst Case Drawdown. A significant gap suggests that while the historical performance was good, a future reshuffling of market conditions could lead to deeper drawdowns.

5. Diversification Analysis: Pearson Correlation

A portfolio is only as strong as its diversification. We calculated the Pearson Correlation Coefficient based on Daily Returns (not equity curves) to assess true independence.

5.1. The Correlation Matrix

We generated a Heatmap to visualize relationships between strategies:

🟥 High Positive Correlation (> 0.7):

Risk: Strategies move in unison. If one fails, the other likely fails.

Action: Consider reducing position size on correlated pairs (e.g., if DAX40 and US500 show high correlation).

⬜ Low/Zero Correlation (-0.3 to 0.3):

Benefit: True diversification. The performance of one strategy does not affect the other.

Observation: Ideally, Gold strategies should show low correlation to Index strategies.

🟦 Negative Correlation (< -0.5):

Benefit: Hedging effect. One strategy tends to profit when the other loses, smoothing the volatility.

6. Conclusion 

Based on the quantitative analysis performed in Python:

Data Integrity: The data pipeline is now robust and scalable for adding future strategies.

Performance: The unified portfolio demonstrates the power of compounding distinct edges.
