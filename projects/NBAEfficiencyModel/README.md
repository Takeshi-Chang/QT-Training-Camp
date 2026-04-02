# NBA Efficiency Modeling: Predicting True Shooting Percentage

NOTE: This is simply an overview of the project. See report/nba_efficiency_report.html for more detail. 

## Overview
This project builds a predictive model for NBA player efficiency (True Shooting Percentage) using shot profile, usage, and other metrics encapsulating on-court tendencies.

The goal was to understand:
- Which player tendencies most influence efficiency
- Whether nonlinear relationships improve predictive performance
- How much of shooting efficiency can realistically be explained using box-score features

---

## Approach

### Feature Selection
Here are a few of the carefully selected interpretable predictors (out of 9 total):
- Free throw rate (`f_tr`)
- 3-point attempt rate (`x3p_ar`)
- Offensive rebounding (`orb_percent`)
- Assist rate (`ast_percent`)

### Modeling Pipeline
- Baseline linear regression
- Polynomial feature expansion (degree = 2)
- Ridge regularization (to retain all predictors while controlling overfitting)
- Out-of-sample evaluation using test RMSE and \(R^2\)

---

## Results

| Model | Test RMSE | Test \(R^2\) |
|------|----------|-------------|
| Baseline (few predictors) | ~4.612 | ~0.067 |
| Final Ridge + Polynomial (deg=2) | **3.945** | **0.317** |

### Key Improvements
- Significant reduction in prediction error (RMSE ↓)
- ~5x increase in explanatory power
- Nonlinear terms improved performance, but higher-order (degree 3) provided negligible gains

---

## Key Insights

- **Free throw rate and 3-point attempt rate** are the strongest drivers of efficiency
- **Steal rate** shows a negative relationship, likely reflecting role/player archetypes
- Some nonlinear effects exist, but diminishing returns appear quickly

---

## Interpretation

Even with nonlinear modeling and regularization:
- The model explains only **~31.7% of variance**
- Indicates that efficiency is influenced by:
  - Shot quality
  - Defensive pressure
  - Team context
  - Unobserved variables not captured in box-score stats

---

## Why Ridge (Not Lasso)?

Ridge was chosen intentionally:
- Preserves all predictors
- Allows analysis of full feature effects
- Avoids dropping variables that were carefully selected for interpretability

---

## Limitations

- Relies only on box-score / aggregated features
- No spatial shot data or tracking data
- Limited ability to capture context (defense, play type, etc.)
- Moderate predictive power suggests missing structure in the data

---

## Future Work

- Incorporate shot location / tracking data (albeit hard to find)
- Explore tree-based models (Random Forest, XGBoost)
- Add interaction-heavy feature engineering
- Evaluate time-series stability across seasons

---

## Tech Stack
See notebooks/nba_efficiency_code.html for all the tools utilized & more detail.

- Python (pandas, numpy)
- scikit-learn 
- statsmodels
