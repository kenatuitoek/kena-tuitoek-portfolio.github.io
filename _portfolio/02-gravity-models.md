---
title: "Gravity Models of African Trade"
excerpt: "PPML gravity models using CEPII/WTO data to quantify how WTO membership and regional trade agreements shape African trade integration."
collection: portfolio
category_label: "Econometrics"
status: "Complete"
accent_color: "#5B8DEF"
tagline: "PPML Estimation with High-Dimensional Fixed Effects"
methods:
  - PPML gravity estimation
  - High-dimensional fixed effects
  - Multilateral resistance controls
  - Partial equilibrium counterfactuals
tools:
  - Stata (ppmlhdfe)
  - R
  - Python
  - CEPII
  - WTO data
tags:
  - gravity model
  - trade
  - PPML
  - panel data
---

## Overview

Built a product-level panel of **~960,000 observations** of African bilateral trade flows and estimated gravity models using Poisson pseudo-maximum likelihood (PPML) with high-dimensional fixed effects to quantify the partial effects of WTO membership vs. regional trade agreements on trade integration.

## Methodology

The gravity model is the workhorse of empirical trade analysis. I estimate:

$$\text{Trade}_{ij,t} = \exp\left(\beta_1 \text{WTO}_{ij,t} + \beta_2 \text{RTA}_{ij,t} + \gamma \mathbf{X}_{ij} + \alpha_{i,t} + \alpha_{j,t}\right) + \varepsilon_{ij,t}$$

Using **PPML** rather than log-linear OLS because:
- It handles zero trade flows (common in African bilateral pairs)
- It's consistent under heteroskedasticity (Santos Silva & Tenreyro, 2006)
- The RESET test confirms adequate functional form

```stata
ppmlhdfe trade wto_both rta ln_dist contig comlang  ///
    , absorb(exp_year imp_year) cluster(pair_id)

* Coefficient interpretation: exp(β)-1 = % trade effect
* E.g. β_wto = 0.35 → WTO membership raises trade by ~42%
```

## Key results

| Variable | Trade effect (%) | Std. Error |
|----------|-----------------|------------|
| WTO (both members) | +42% | 8 |
| Regional trade agreement | +67% | 12 |
| Contiguity | +89% | 15 |
| Common language | +44% | 9 |
| Colonial ties | +71% | 14 |

RTAs have a larger partial effect on African trade than WTO membership alone, suggesting regional integration agreements are the more powerful channel for trade expansion on the continent.

## Data construction

- **Trade flows:** CEPII bilateral trade database, product-level aggregated to country pairs
- **Gravity variables:** CEPII GeoDist (distance, contiguity, language, colonial links)
- **Policy indicators:** WTO membership dates, RTA/PTA indicators from WTO RTA database
- **Fixed effects:** Exporter×year and importer×year to control for multilateral resistance

## Robustness checks

- RESET test for functional form (PPML passes, OLS fails)
- Comparison with OLS on log(1+trade) — substantial bias from zeros
- Alternative clustering (country-pair vs. country-level)
- Phased-in RTA effects to test for anticipation
