# Crystal Study — EDA & PCA Analysis

> Exploratory data analysis and Principal Component Analysis on a physicochemical crystal dataset. Covers data preprocessing, outlier detection, variable encoding, standardization, and dimensionality reduction.

## Overview

This project characterizes and classifies crystals based on their chemical composition and physical properties. The full pipeline goes from raw data exploration to PCA-based dimensionality reduction using the NIPALS algorithm.

## Dataset

Multi-variable dataset with the following features:

| Group | Variables | Type |
|---|---|---|
| Chemical composition | RI, Na, Mg, Al, Si, K, Ca, Ba, Fe | Numerical |
| Physical properties | Type, hardness, density | Numerical |
| Visual characteristics | color, transparency | Categorical |

> `thermal_exp` was removed due to unknown domain meaning.

## Analysis Pipeline

1. **EDA** — Descriptive statistics, coefficient of variation, near-constant variable detection
2. **Outlier Detection** — Scaled boxplots + histograms; `K` values > 3 flagged as inconsistent → replaced with `NA`
3. **Variable Encoding** — Categorical variables (color, transparency) converted to binary dummy variables
4. **Standardization** — Z-score autoscaling (μ = 0, σ = 1) across all numerical features
5. **PCA (NIPALS)** — Handles missing values in `K`; 7 components retained via Kaiser criterion
6. **Validation** — RSS-based moderate outlier detection per observation

## Key Results

- **7 principal components** → **78.98% cumulative variance**
- **PC1** (22.6%): driven by RI and Ca — refraction/density axis
- **PC2** (14.5%): Mg vs Al & Ba chemical contrast
- **PC3–PC4**: minority elements K and Fe variability
- **Moderate outliers detected**: `id132`, `id150`, `id145`

## Setup

### Requirements

```r
install.packages(c("FactoMineR", "factoextra", "ggplot2", "dplyr", "tidyr"))
