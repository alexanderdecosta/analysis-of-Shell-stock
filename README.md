# Shell vs Natural Gas and Renewables Performance Analysis

This repository contains a comprehensive analysis comparing Shell's equity performance to natural gas prices and renewable-focused equities over the period 2006–2025. The analysis includes normalized price performance, risk-return metrics, regime-based correlation analysis, and regression modeling to understand the relationship between LNG-focused equities and natural gas prices.

## Overview

The goal of this analysis is to:

- Compare Shell's performance to renewable-focused equities.
- Assess Shell's sensitivity to natural gas price movements.
- Evaluate co-movement between Shell and natural gas across different market regimes (high, medium, low gas prices).
- Quantify predictive relationships using linear regression.

The results highlight Shell's ability to maintain consistent growth across market cycles, the comparative performance of renewable equities, and the nuanced relationship between LNG equities and natural gas prices.

## Data

- **Equities:**
  - LNG-focused: Shell (SHEL)
  - Renewable-focused: Brookfield Renewable (BEP), Boralex (BLX.TO), NextEra Energy (NEE)
- **Commodity:** Natural Gas (Henry Hub, NG=F)
- **Time period:** 2006–2025
- **Sources:** Yahoo Finance via `yfinance` Python package

### Data Coverage Summary

| Name                 | Ticker | First Date | Last Date | Total Obs | NA Count |
|----------------------|--------|------------|-----------|-----------|----------|
| Shell                | SHEL   | 2006-01-03 | 2025-12-31 | 5031      | 93       |
| Brookfield Renewable | BEP    | 2006-01-03 | 2025-12-31 | 5031      | 93       |
| Boralex              | BLX.TO | 2006-01-03 | 2025-12-31 | 5020      | 104      |
| NextEra Energy       | NEE    | 2006-01-03 | 2025-12-31 | 5031      | 93       |

## Analysis

### Normalized Price Performance

Normalized price charts allow direct comparison of equity growth over the analysis period. Shell demonstrates consistent growth across the cycle, while renewable equities have outperformed Shell on average by ~4% per year with slightly lower volatility.

### Risk-Return Summary

**Training period (2006–2015)**

| Ticker | Annual Return | Annual Volatility |
|--------|---------------|-----------------|
| NEE    | 16.2%         | 23.5%           |
| BLX.TO | 11.4%         | 34.8%           |
| BEP    | 11.3%         | 23.5%           |
| SHEL   | 9.2%          | 28.1%           |

**Test period (2015–2025)**

| Ticker | Annual Return | Annual Volatility |
|--------|---------------|-----------------|
| NEE    | 15.7%         | 24.5%           |
| BLX.TO | 14.8%         | 28.3%           |
| BEP    | 13.0%         | 29.9%           |
| SHEL   | 9.5%          | 31.1%           |

### Correlation Analysis

- **3-Month rolling correlation (Shell vs Gas):**
  - Train: 0.2830
  - Test: 0.0561

- **Regime-based correlations:**

| Gas Regime | Train  | Test  |
|------------|--------|-------|
| High       | 0.3612 | 0.3658 |
| Medium     | 0.4202 | 0.1501 |
| Low        | -0.1794| 0.1651 |

Analysis indicates moderate co-movement between Shell and natural gas in high-price regimes, but overall weak predictive power.

### Linear Regression Analysis

A linear regression model was fitted with interaction terms for medium and high gas regimes:

R_LNG = α + βR_gas + γ_mediumR_gasD_medium + γ_highR_gas*D_high + ε


**Key Findings:**

- Base effect of gas returns (low regime): -0.0317
- Additional effect in medium regime: 0.2922
- Additional effect in high regime: 0.2567

**High Regime Performance:**

| Period         | N observations | R²    | RMSE     |
|----------------|----------------|-------|----------|
| Train (2006-2015)| 12           | 0.0759| 0.1375  |
| Test (2015-2025) | 13           | 0.0195| 0.1039  |

The low R² indicates that while Shell moves somewhat with natural gas in high-price regimes, the predictive power is weak.

## Conclusions

- Shell has maintained steady growth through market cycles, demonstrating resilience against volatile natural gas prices.
- Renewable-focused equities have outperformed Shell in terms of annual returns while exhibiting similar or lower volatility.
- Correlation and regression analyses show some co-movement between Shell and natural gas in high-price regimes, but predictive power remains low.
- Overall, Shell’s strategy appears to balance exposure to energy markets while maintaining stable growth.

## Usage

Clone this repository and run the Jupyter notebook `Shell_vs_Gas_and_Renewables.ipynb` to reproduce the analysis and charts.  

```bash
git clone <repository-url>
cd <repository-folder>
jupyter notebook

