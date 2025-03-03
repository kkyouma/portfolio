---
title: ML Strategy pattern
publishDate: 2020-03-04 00:00:00
img: /assets/stock-3.jpg
img_alt: Pearls of silky soft white cotton, bubble up under vibrant lighting
description: |
  A minimal implementation of the Strategy Design Pattern for machine learning workflows.
tags:
  - Machine learning
  - Data science
  - Pandas
  - Design Patterns
---

# ML Strategy Pattern: A Study in Model Management 🧠🔧

A minimal implementation of the **Strategy Design Pattern** for machine learning workflows. Built for educational purposes to demonstrate clean, modular, and extensible code in data science projects.

---

## Features ✨

### Implemented

- **Strategy Pattern Framework**
  - Swappable model strategies (`XGBRegressorStrategy`, `RFRegressorStrategy`)
  - Central `ForecastingContext` class to manage models/data
- **Core ML Operations**
  - Training/validation/test splits
  - Hyperparameter tuning via `GridSearchCV`
  - Metrics calculation (MAE, MSE, R², MAPE)
  - Model persistence (save/load `.pkl` files)
- **Dataset**  
  Uses [Store Sales Time Series Forecasting data from Kaggle](https://www.kaggle.com/competitions/store-sales-time-series-forecasting/data).  
  Required file: `train.csv` (place in `data/raw/`)

### Missing (Study Opportunities) 🔍

- 🚫 **Unit tests** (critical gap!)
- 🚫 Consistent preprocessing persistence (RF encoder not saved)
- 🚫 Logging system (currently uses `print`)
- 🚫 Time-series specific validation
- 🚫 Error handling for edge cases
- 🚫 Pipeline integration for preprocessing
