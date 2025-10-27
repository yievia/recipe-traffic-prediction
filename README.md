# recipe-traffic-prediction
Predicting recipe website traffic (High vs Low) using nutritional and categorical features with Logistic Regression, Decision Tree, and Random Forest.

## Project Overview

This project predicts whether a recipe will experience high or low traffic based on its nutritional and categorical attributes.
The business objective is to help content managers prioritize recipes likely to attract high user engagement.

## Business Goals

1. Classify recipes as *High Traffic* or *Low Traffic* using supervised machine learning models.
2. Identify key drivers of recipe popularity (e.g., food category, protein ratio, sweetness density).
3. Establish a performance KPI — High Traffic Conversion Rate (HTCR) to align model evaluation with business outcomes.
4. Achieve at least 80% precision, ensuring that recipes predicted as “High Traffic” are indeed likely to perform well.


## Dataset

* Source: Recipe Site Traffic dataset (947 rows × 8 columns)
* Features:

* `calories`, `carbohydrate`, `sugar`, `protein`, `servings`, `category`
* Engineered ratios: `protein_ratio`, `carb_protein_ratio`, `sweetness_density`
* Target Variable: `high_traffic` (`High` → 1, `Low` → 0)


## Data Cleaning & Preprocessing

* Converted categorical features using one-hot encoding
* Handled missing nutritional data using category-servings mean imputation
* Applied Yeo-Johnson transformation to correct skewed numeric distributions
* Dropped invalid or incomplete rows (`NaN` after imputation)
* Split dataset into train (80%) and test (20%) sets


## Models Developed

Three supervised classification models were trained and evaluated:

* Logistic Regression (baseline)
* Decision Tree Classifier
* Random Forest Classifier


## Model Evaluation Results

| Model               | Accuracy  | Precision | Recall    | F1-Score  |
| :------------------ | :-------- | :-------- | :-------- | :-------- |
| Logistic Regression | 0.676     | 0.877     | 0.533     | 0.663     |
| Decision Tree       | 0.726     | 0.790     | 0.738     | 0.763     |
| Random Forest       | 0.687     | 0.758     | 0.701     | 0.728     |


Confusion Matrices:

* Logistic Regression → `[[64, 8], [50, 57]]`
* Decision Tree → `[[51, 21], [28, 79]]`
* Random Forest → `[[48, 24], [32, 75]]`



## Feature Importance Insights

### Logistic Regression (Top Predictors)

* Positive drivers: Vegetable, Potato, Pork, One Dish Meal, Meat, Dessert
* Negative drivers: Breakfast, sweetness_density (low sugar density)

### Decision Tree

Top numerical features: `calories per serving`, `carb_protein_ratio`, `protein_ratio`, `sweetness_density`

### Random Forest

Consistent top features: `protein_ratio`, `carb_protein_ratio`, `sweetness_density`, `calories per serving`

Interpretation:
High-protein, balanced carb-to-protein recipes, especially from *Vegetable*, *Potato*, and *Pork* categories, are most likely to achieve higher traffic.


## Business KPI – High Traffic Conversion Rate (HTCR)

| Model               | HTCR     | Interpretation                            |
| :------------------ | :------- | :---------------------------------------- |
| Logistic Regression | 7.13     | Excellent precision — few false positives |
| Decision Tree       | 3.76     | Moderate, some misclassifications         |
| Random Forest       | 3.13     | Acceptable but less consistent            |

Target KPI: HTCR ≥ 4.0
Logistic Regression meets business performance target.


## Key Findings

* Logistic Regression provides the most balanced and business-relevant predictions, achieving an HTCR above 4.
* Decision Tree and Random Forest slightly overfit but offer interpretability on feature interactions.
* Protein ratio and food category remain the most influential predictors of high traffic.



## Recommendations

* Deploy Logistic Regression model for ongoing prediction of high-traffic recipes.
* Periodically retrain with new traffic data to maintain model accuracy.
* Collect additional features such as:

  * *Recipe preparation time*
  * *Ingredient cost per serving*
  * *User engagement metrics (time on page, likes, shares)*
* Use model outputs to optimize homepage recipe placement and marketing content.


## Tech Stack

* Language: Python (Pandas, NumPy, Scikit-Learn, Seaborn, Matplotlib)
* IDE: Jupyter Notebook
* Version Control: GitHub
