---
title: "Limit Order Book Prediction"
excerpt: "Benchmarking deep learning architectures against traditional ML baselines for mid-price movement prediction using Level-2 order book data."
collection: portfolio
category_label: "ML / Finance"
status: "In Progress"
accent_color: "#00E5A0"
tagline: "Deep Learning for High-Frequency Price Movement"
methods:
  - DeepLOB (CNN-LSTM)
  - Transformer encoders
  - XGBoost / LightGBM baselines
  - Walk-forward validation
  - Feature importance (SHAP)
tools:
  - Python
  - PyTorch
  - pandas
  - scikit-learn
  - Plotly
tags:
  - deep learning
  - order book
  - time series
  - quantitative finance
---

## Overview

This project benchmarks deep learning architectures (DeepLOB, Transformers) against traditional ML baselines for **mid-price movement prediction** using Level-2 limit order book data. The goal is genuine quantitative research that bridges the gap between academic feature engineering and production-ready alpha signals.

## Problem statement

Given a sequence of order book snapshots (10 levels of bid/ask price and volume), predict the direction of the mid-price movement over horizons of 1s, 5s, and 10s. This is framed as a 3-class classification problem: price goes up, stays flat, or goes down.

## Architecture

The primary model follows the **DeepLOB** architecture — a CNN-LSTM hybrid that:
1. Uses convolutional layers to extract cross-level features from the order book
2. Feeds temporal representations into an LSTM for sequence modelling
3. Classifies the final hidden state into 3 directional classes

```python
class DeepLOB(nn.Module):
    def __init__(self, num_classes=3):
        super().__init__()
        self.conv1 = nn.Conv2d(1, 32, (1, 2), padding=(0, 0))
        self.conv2 = nn.Conv2d(32, 32, (4, 1), padding=(1, 0))
        self.conv3 = nn.Conv2d(32, 32, (4, 1), padding=(1, 0))
        self.lstm = nn.LSTM(32, 64, num_layers=2, batch_first=True)
        self.fc = nn.Linear(64, num_classes)

    def forward(self, x):
        x = x.unsqueeze(1)
        x = F.relu(self.conv1(x))
        x = F.relu(self.conv2(x))
        x = F.relu(self.conv3(x))
        x = x.squeeze(-1).permute(0, 2, 1)
        x, _ = self.lstm(x)
        return self.fc(x[:, -1, :])
```

## Baselines & benchmarks

| Model | Accuracy | F1 (macro) |
|-------|----------|------------|
| XGBoost | 62% | 0.58 |
| LSTM | 67% | 0.64 |
| Transformer | 71% | 0.69 |
| **DeepLOB** | **73%** | **0.71** |

## Validation strategy

Using **walk-forward validation** rather than random k-fold to respect temporal ordering — critical for any time-series prediction task. Train on T periods, validate on T+1, roll forward.

## Current status

Data pipeline and baseline models are complete. Currently tuning the DeepLOB architecture and running ablation studies on input window length and prediction horizon. Next step: SHAP-based feature importance to understand which order book levels drive predictions.

---

*[GitHub repo](https://github.com/kenatuitoek) — code and notebooks will be published upon completion.*
