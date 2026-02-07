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

**Note:** Figures of normalized stock returns are available and can be viewed in the Jupyter notebook `Shell_vs_Gas_and_Renewables.ipynb`.

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

Analysis indicates moderate co-movement between Shell and natural gas in high-price regimes, but overall predictive power is weak.

### Linear Regression Analysis

A linear regression model was fitted to quantify the relationship between 3-month Shell equity returns and natural gas returns with interaction terms for medium and high gas price regimes. The model can be expressed as:

**Regression Model:**

R_LNG = alpha + beta * R_gas + gamma_medium * (R_gas * D_medium) + gamma_high * (R_gas * D_high) + epsilon

Where:

- R_LNG = Shell equity 3-month return  
- R_gas = 3-month natural gas return  
- D_medium, D_high = regime dummies for medium and high gas price regimes  
- alpha, beta, gamma_medium, gamma_high = regression coefficients  
- epsilon = residual error

**Key Findings (All Regimes):**

| Effect | Coefficient |
|--------|------------|
| Base effect (low regime) | -0.0317 |
| Medium regime adjustment  | 0.2922 |
| High regime adjustment    | 0.2567 |

**Interpreted Total Effects by Regime:**

| Regime | Total β |
|--------|----------|
| Low    | -0.0317 |
| Medium | 0.2604  |
| High   | 0.2250  |

**Performance Metrics (High Regime Only):**

| Period         | N obs | R²    | RMSE     |
|----------------|-------|-------|----------|
| Train (2006-2015)| 12  | 0.0759| 0.1375  |
| Test (2015-2025) | 13  | 0.0195| 0.1039  |

**Full Regression Discussion:**

- The low R² across all regimes suggests that natural gas returns explain only a small portion of Shell’s equity return variability.  
- Positive coefficients in medium and high regimes indicate that Shell tends to move in the same direction as gas when prices are elevated.  
- Negative base effect in the low regime implies slight inverse movement when natural gas prices are low.  
- Overall, the linear model captures some regime-specific sensitivity but is limited in predictive power, highlighting the influence of broader company-specific and market factors.

## Conclusions

- Shell has maintained steady growth through market cycles, demonstrating resilience against volatile natural gas prices.  
- Renewable-focused equities have outperformed Shell in terms of annual returns while exhibiting similar or lower volatility.  
- Correlation and regression analyses show modest co-movement between Shell and natural gas in high-price regimes, but predictive power is low.  
- Shell’s performance appears driven by a combination of energy exposure and company-specific strategies rather than purely natural gas movements.

## Usage

Clone this repository and run the Jupyter notebook `Shell_vs_Gas_and_Renewables.ipynb` to reproduce the analysis and charts.  

```bash
git clone https://github.com/alexanderdecosta/analysis-of-Shell-stock.git
cd analysis-of-Shell-stock
jupyter notebook
