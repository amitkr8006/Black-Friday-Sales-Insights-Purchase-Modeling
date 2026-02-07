# Black Friday Sales Insights & Purchase Modeling

## Overview
This project analyses a large Black Friday retail transactions dataset to understand spending patterns across customer segments, detect and treat extreme purchase outliers, and build a simple baseline regression model to quantify how basic attributes relate to purchase value. The work is packaged as a Quarto report and rendered to an HTML deliverable.

## Problem Statement
Retail datasets often contain strong segment-level patterns (who spends more) alongside heavy-tailed purchase behaviour (rare, very high transactions). The goal here was to:
- Profile total spending by key customer segments (Gender, Age, City category)
- Identify extreme purchase outliers and assess their impact
- Build a baseline model as a starting point for explaining purchase value

## Data Summary
- Transaction-level dataset: 550,068 rows × 12 columns
- Key fields include: User_ID, Product_ID, Gender, Age, Occupation, City_Category, Marital_Status, Product_Category_1/2/3, and Purchase

## Tools & Methods
### Tools
- R + Quarto (HTML report)
- Libraries: tidyverse, dplyr, tibble, ggplot2, scales, kableExtra, performance

### Data Preparation
- Converted categorical variables to factors (Gender, Age, City_Category, Occupation, Marital_Status, Product_Category_1)
- Dropped Product_Category_2, Product_Category_3, and Stay_In_Current_City_Years to keep analysis focused
- Checked missing values and verified structure

### Exploratory Data Analysis (EDA)
- Computed descriptive statistics for Purchase (mean, median, standard deviation)
- Aggregated and visualised total Purchase by:
  - Gender
  - Age group
  - City_Category
- Charts were created using ggplot2 with formatted axes for readability

### Outlier Detection
- Used the IQR method on Purchase:
  - Computed Q1, Q3, IQR, and an upper bound
  - Flagged and removed extreme-high Purchase values
- Removed 2,677 rows (550,068 → 547,391) after filtering
- Defined high-value purchases using the 90th percentile and compared the share of high-value transactions across age groups

### Baseline Modeling
- Built a linear regression model:
  - Purchase ~ Gender + Age + City_Category
- Converted categorical factors to numeric codes for modeling
- Evaluated with summary statistics and performance metrics:
  - R² ≈ 0.0076 (very low explanatory power)
  - RMSE ≈ 4774.66
  - AIC/BIC reported for model comparison context

## Key Findings
- Total spending concentration:
  - Males contributed the majority of total purchase value (~78%)
  - Age group 26–35 had the highest total spend
  - City Category B showed the highest total purchase value
- Outliers materially exist in Purchase and were treated using an IQR-based approach
- The baseline regression is statistically significant but explains <1% of purchase variance, indicating that richer feature sets and/or non-linear models are needed for stronger prediction.

## Deliverables
- A Quarto-rendered HTML report containing:
  - The full workflow
  - Data cleaning steps and summary statistics
  - EDA visualisations
  - Outlier detection logic and filtered dataset size
  - Regression output and model evaluation metrics

## Limitations & Next Steps
- The regression only includes a small set of predictors; future iterations can:
  - Add product categories, occupation, interactions, and engineered features
  - Try non-linear models (tree-based, boosted methods)
  - Validate with train/test splits and cross-validation
  - Explore segment-specific models (e.g., by city category or age bands)
