---
title: "Portfolio Risk Modelling"
excerpt: "Factor models, GARCH volatility estimation, and bootstrap inference for multi-asset portfolio construction and risk budgeting."
collection: portfolio
category_label: "Finance"
status: "Complete"
accent_color: "#C792EA"
tagline: "Factor Models & Non-Parametric Volatility Analysis"
methods:
  - Fama-French 3-factor model
  - GARCH(1,1) volatility
  - Bootstrap confidence intervals
  - Risk parity allocation
tools:
  - Python
  - R
  - numpy
  - statsmodels
  - arch
  - matplotlib
tags:
  - portfolio construction
  - GARCH
  - factor models
  - risk management
---

## Overview

Factor model construction and non-parametric statistical tests to analyse asset return distributions and **volatility dynamics** for portfolio construction. Implemented Fama-French factor decomposition, rolling variance estimation, and bootstrap-based inference for risk budgeting.

## GARCH volatility estimation

```python
from arch import arch_model
import numpy as np

# Fit GARCH(1,1) to daily returns
garch = arch_model(returns, vol='Garch', p=1, q=1, 
                   mean='AR', lags=1, dist='t')
result = garch.fit(disp='off')

# Extract conditional volatility
cond_vol = result.conditional_volatility
annualised_vol = cond_vol * np.sqrt(252)

# Forecast 10-day ahead variance
forecast = result.forecast(horizon=10)
var_10d = forecast.variance.iloc[-1].values
```

## Factor decomposition

Decomposed asset returns using the Fama-French 3-factor model:

$$R_i - R_f = \alpha_i + \beta_{i,\text{MKT}}(R_m - R_f) + \beta_{i,\text{SMB}} \cdot \text{SMB} + \beta_{i,\text{HML}} \cdot \text{HML} + \varepsilon_i$$

This separates systematic risk (market, size, value) from idiosyncratic risk, enabling more informed portfolio allocation decisions.

## Bootstrap inference

Used **block bootstrap** (preserving autocorrelation structure) to construct confidence intervals for Sharpe ratios and volatility estimates — avoiding the normality assumption that standard parametric tests rely on.

## Key takeaways

- GARCH conditional volatility significantly outperforms rolling-window estimates for risk forecasting
- Factor-adjusted returns reveal that apparent alpha often disappears after controlling for size and value tilts
- Bootstrap CIs for Sharpe ratios are substantially wider than parametric ones — a reminder that back-tested performance is noisier than it appears
