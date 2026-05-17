# 🏠 Predictive Modeling of Real Estate Pricing

A from-scratch implementation of linear regression models to predict real estate prices — built without scikit-learn, using only NumPy and Pandas.

---

## 📌 Project Overview

This project explores three perspectives on the same regression problem:

| View | Approach |
|---|---|
| **Gradient Descent** | Custom `MultiLinearRegressionGD` class trained via iterative weight updates |
| **Statistical** | Closed-form OLS using SXX / SXY formulas (simple linear regression) |
| **Numerical** | Normal equations solved via matrix algebra (`np.linalg.solve`) |

Regularization is also implemented from scratch:
- **Ridge Regression** — L2 penalty via gradient descent
- **Lasso Regression** — L1 penalty via gradient descent

```

## 📊 Dataset

The dataset (`real_estate_S.xlsx`) contains property listings with the following features:

| Feature | Type | Description |
|---|---|---|
| `Area_sqft` | Numeric | Property area in square feet |
| `Bedrooms` | Numeric | Number of bedrooms |
| `Bathrooms` | Numeric | Number of bathrooms |
| `Age` | Numeric | Property age (years) |
| `Distance_to_Center` | Numeric | Distance from city center (km) |
| `Neighborhood` | Categorical | Beach / Downtown / Suburb / Industrial / Rural |
| `Property_Type` | Categorical | Villa / House / Apartment / Townhouse |
| `Garage_Type` | Categorical | Attached / Detached / None |
| `Has_Pool` | Binary | Yes / No |
| `Price` | Numeric | **Target variable** — property sale price |

> ⚠️ The data file is excluded from version control. Add it to `data/` before running the notebook.

---

##  Data Preprocessing Pipeline

1. **Missing value imputation** — grouped means/medians for numeric columns; mode imputation for categoricals
2. **Outlier detection & removal** — IQR-based method on `Area_sqft` and `Distance_to_Center`
3. **Feature engineering** — `Distance_group` (Close / Moderate / Far) bucketed from `Distance_to_Center`
4. **Encoding** — ordinal encoding for `Neighborhood` and `Property_Type` (price-correlated); one-hot for `Garage_Type`
5. **Normalization** — Z-score standardization (fit on train, applied to test)

---

## 🤖 Models

### Custom Gradient Descent (`MultiLinearRegressionGD`)
- Supports **no regularization**, **Ridge (L2)**, and **Lasso (L1)**
- Configurable: `learning_rate`, `epochs`, `tolerance`
- Outputs: loss curve, predicted vs actual, residuals, coefficient bar chart

### Statistical Simple Linear Regression (`StatisticalModel`)
- Closed-form solution using SXX / SXY
- Best single predictor: `Area_sqft`

### Numerical Simple Linear Regression (`SimpleLinearRegressionNumericalView`)
- Normal equations via `np.linalg.solve`
- Step-by-step output of summations and matrix form

### Ridge & Lasso (Model Comparison)
Three model specifications compared across Ridge and Lasso:
- **Model 1** — Best single predictor (`Age`)
- **Model 2** — Full model (all features)
- **Model 3** — Domain knowledge subset (`Area_sqft`, `Bedrooms`, `Age`, `Distance_to_Center`)

---

## 📈 Interactive Visualizations (Plotly)

| Chart | Description |
|---|---|
| Correlation Heatmap | Numeric variable correlations |
| Scatter Plot | Selectable feature vs Price with regression line |
| GD Convergence | MSE loss per iteration across all 3 model specs |
| Residual Plots | Ridge residuals for all 3 specifications |
| Coefficient Chart | Beta comparison across model specifications |

---

##  Dependencies

See [`requirements.txt`](requirements.txt)

---
