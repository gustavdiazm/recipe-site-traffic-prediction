# Recipe High-Traffic Prediction

## Project Overview

This project aims to predict whether a recipe will generate high traffic on a cooking website. By analyzing recipe characteristics such as nutritional content, category, and serving size, I have developed a classification model that helps the product team select recipes most likely to drive user engagement and site traffic.

The model achieves 85.26% precision, exceeding the target of 80%, making it a reliable tool for replacing manual recipe selection with a data-driven approach.
Business Problem

The product team currently selects the daily homepage recipe based on personal preference and intuition. This subjective approach often results in inconsistent traffic performance. The goal of this project was to build a predictive model that:

- Identifies recipes with high traffic potential with at least 80% precision

- Reduces the risk of showcasing low-performing recipes

- Provides actionable insights to optimize homepage content strategy

# Dataset

The dataset contains recipe information with the following columns:
Column	Description
Recipe	Unique recipe identifier
Calories	Calorie count per serving
Carbohydrate	Carbohydrate content (grams)
Sugar	Sugar content (grams)
Protein	Protein content (grams)
Category	Recipe category (e.g., Meat, Vegetables, Breakfast)
Servings	Number of servings per recipe
High_traffic	Target variable: 'High' if recipe generated high traffic

Initial shape: 947 rows, 8 columns
After cleaning: 895 rows, 8 columns (52 rows with missing values removed)

Data Validation & Cleaning

- Removed 52 rows with missing values in numerical columns (Calories, Carbohydrate, Sugar, Protein)

- Cleaned the Servings column by removing text like "as a snack" and converting to numeric

- Standardized categories: merged 'Chicken Breast' into 'Chicken' category

- Filled missing values in High_traffic with 'Not High'

Exploratory Analysis

Target Variable Distribution:

- High traffic recipes: ~59.8%

- Not high traffic recipes: ~40.2%

Correlation Analysis:

- Negligible linear relationships between numeric variables

- This suggests each predictor contributes independently, making their combination potentially powerful for modeling

Feature Distribution:

- Applied Yeo-Johnson PowerTransformer for better normal distribution of numerical features

- Transformation applied after train-test split to avoid data leakage

Category Analysis:

- High-performing categories: Meat, Vegetables, Pork, One Dish Meal, Potato

- Low-performing categories: Breakfast, Beverages

Servings Analysis:

- Slight trend: more servings = marginally higher traffic probability

- Overall, a weaker predictor compared to Category

# Models

Baseline Model: Logistic Regression

- Selected for simplicity, interpretability, and low computational cost

- Provides clear performance benchmark

- Coefficients directly reveal which features drive traffic

Comparison Model: Random Forest

- Tests whether non-linear interactions yield performance gains

- Robust to outliers

- Handles mixed data types well

- Provides feature importance insights

Key Insight: Logistic Regression was selected as the final model because it delivers higher precision (85.1% vs 80.8%) while maintaining the same recall. This means fewer false positives — fewer unpopular recipes mistakenly promoted on the homepage.
Business Impact

- 85.26% confidence that recommended recipes will generate high traffic

- Out of every 10 recipes selected, 8 to 9 will deliver the desired traffic boost

- Surpasses the product team's 80% precision target

- Objective, data-driven recommendations replace subjective selection

# Key Finding

The most important factor for predicting high traffic is the recipe category. Categories like Meat, Vegetables, Pork, One Dish Meal, and Potato are strongly associated with high traffic, while Breakfast and Beverages tend to underperform.
Recommendations

1. Deploy Immediately

Replace manual selection with the model's probability scores. Monitor traffic performance for the first two weeks.

2. Leverage Category Insights

Prioritize top-performing categories on the homepage and develop strategies around these high-impact categories.

3. Continuous Improvement

- Fine-tune the decision threshold if required
- Build a dashboard to monitor precision and F1-score KPIs
- Retrain the model monthly to maintain performance

4. Add New Features

Incorporate additional data such as:

- Preparation time
- Cost per serving
- Recipe difficulty
- User ratings

Technologies Used

- Python

- Pandas / NumPy — Data manipulation

- Scikit-learn — Preprocessing, modeling, evaluation

- PowerTransformer (Yeo-Johnson) — Feature transformation

- Matplotlib / Seaborn — Visualizations
