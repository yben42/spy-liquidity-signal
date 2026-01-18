# SPY vs Reverse Repo Signal Analysis

This project explores the relationship between **U.S. Federal Reserve Reverse Repo operations** and **SPY (S&P 500 ETF) price behavior**, and tests a simple **signal-based trading strategy** derived from liquidity dynamics.

The analysis combines macroeconomic data with market prices to evaluate whether changes in liquidity conditions can be used as a directional signal.

---

## Overview

The core idea behind this project is:
- Reverse Repo balances reflect short-term liquidity conditions
- Liquidity expansion/contraction may influence equity market direction
- Aligning trends in liquidity and price momentum may improve timing versus buy-and-hold

To test this, the project:
1. Collects SPY price data
2. Collects Reverse Repo daily totals from FRED
3. Normalizes and inverts liquidity data
4. Applies EMA smoothing and gradient-based signals
5. Backtests a simple long-only strategy
6. Compares results against buy-and-hold SPY

---

## Data sources

- **SPY daily prices**  
  Retrieved via the **Tiingo API**

- **Reverse Repo operations (RRPONTSYD)**  
  Retrieved from the **Federal Reserve Economic Data (FRED)** API

Date range analyzed:
- April 2024 – May 2025

---

## Methodology

- Normalize SPY prices and Reverse Repo balances (z-score)
- Invert Reverse Repo series to represent liquidity availability
- Apply exponential moving averages (EMA)
  - SPY EMA: 14-day
  - Reverse Repo EMA: 30-day
- Compute gradients of smoothed series
- Generate a **BUY signal** when:
  - SPY momentum is positive, and
  - Liquidity momentum is improving

To avoid look-ahead bias:
- Signals are **shifted by one trading day** before execution

---

## Strategy logic

- **Signal ON** → Long SPY
- **Signal OFF** → Out of market
- No leverage
- No shorting
- No transaction costs modeled

Performance is evaluated using:
- Cumulative returns
- Sharpe ratio
- Win rate
- Drawdown
- Exposure (% of days invested)

Both **realistic (shifted)** and **leaked (unshifted)** signals are compared to illustrate the impact of look-ahead bias.

---

## Visualizations

The project produces multiple plots, including:
- Normalized SPY vs inverted Reverse Repo EMAs
- Gradient-colored momentum overlays
- Signal vs buy-and-hold cumulative returns
- Strategy drawdowns
- BUY / SELL signal markers on SPY price
- Recent signal status summaries

---

## Results (high-level)

- Signal-based strategy exhibits different risk/return characteristics compared to buy-and-hold
- Liquidity-aligned momentum improves selectivity but reduces market exposure
- Performance is sensitive to smoothing parameters and thresholds
- Demonstrates the importance of avoiding future data leakage in strategy design

This project is **exploratory**, not predictive.

---

## Technologies used

- Python
- pandas, numpy
- requests
- matplotlib
- yfinance
- scikit-learn (metrics)

---

## Notes & limitations

- No transaction costs or slippage modeled
- SPY used as a proxy for the S&P 500
- Strategy is illustrative and not optimized
- Results are period-dependent

---

## Disclaimer

This project is provided **for educational and research purposes only**.  
It does **not** constitute financial advice or a recommendation to trade securities.

All analysis is retrospective and illustrative.  
Use at your own risk.

---

© 2024–2025 Benjamin Yiu
