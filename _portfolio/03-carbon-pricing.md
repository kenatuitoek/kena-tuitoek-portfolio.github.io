---
title: "Carbon Pricing & Trade Competitiveness"
excerpt: "Empirical analysis of how carbon pricing mechanisms (EU ETS, CBAM) affect exports in energy-intensive, trade-exposed sectors."
collection: portfolio
category_label: "Policy / Econometrics"
status: "Complete"
accent_color: "#FF6B6B"
tagline: "EU ETS / CBAM Impact on EITE Sectors"
methods:
  - Systematic literature review
  - Panel data analysis
  - Difference-in-differences
  - Sector-level trade decomposition
tools:
  - R (ggplot2, fixest)
  - Python
  - World Bank Carbon Pricing Dashboard
tags:
  - carbon pricing
  - CBAM
  - EU ETS
  - trade policy
  - climate economics
---

## Overview

Combined a **systematic literature review** with original empirical analysis to assess how carbon pricing mechanisms — carbon taxes, the EU ETS, and the Carbon Border Adjustment Mechanism (CBAM) — affect export competitiveness in energy-intensive, trade-exposed (EITE) sectors.

## Research question

Does carbon pricing cause measurable **carbon leakage** — i.e., do firms in carbon-priced jurisdictions lose export share to competitors in unregulated markets?

## Methodology

### Systematic review

Followed PRISMA guidelines to identify and synthesise the empirical literature on carbon pricing and trade. Key findings from the literature:
- Most studies find **small or statistically insignificant** competitiveness effects
- Effects are concentrated in a handful of sectors (steel, cement, aluminium)
- Free allocation of permits substantially mitigates leakage

### Empirical analysis

Built sector-level panels merging trade data with carbon pricing indicators across jurisdictions:

```python
import pandas as pd
from fixest import feols

# Sector-level panel: exports ~ carbon_price + controls
model = feols(
    'ln_exports ~ carbon_price_eur + i(eite) + ln_gdp_exp + ln_gdp_imp'
    ' | sector_pair + year',
    data=df,
    vcov={'CRV1': 'pair_sector'}
)
```

## Key findings

| Sector | Est. leakage (%) | Confidence |
|--------|------------------|------------|
| Steel | −3.2% | 95% CI |
| Cement | −1.8% | 90% CI |
| Chemicals | −2.4% | 92% CI |
| Aluminium | −4.1% | 88% CI |
| Paper | −0.9% | 85% CI |

Carbon price coefficients for EITE sectors are **negative but economically small** — consistent with the literature finding limited leakage. The CBAM is designed to address precisely this residual gap.

## Digital infrastructure component

A separate component of this research maps the **digital infrastructure** underpinning EU ETS and CBAM compliance systems, and proposes a cyber capacity-building framework for EU–Africa trade governance.
