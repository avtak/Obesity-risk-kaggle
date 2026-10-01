# Obesity Risk Prediction from Lifestyle Factors

Predicting obesity from eating habits, physical activity, family history and demographics, comparing four tree-based classifiers.

## Dataset

[UCI ML Repository: Estimation of obesity levels based on eating habits and physical condition](https://archive.ics.uci.edu/dataset/544/estimation+of+obesity+levels+based+on+eating+habits+and+physical+condition) (id 544): 2,111 records, 2,087 after removing duplicates, 17 attributes. Target: obese (any `Obesity_Type_*` class) vs. not.

## Approach

- **Features:** 14 lifestyle and demographic attributes. Height and weight are excluded because the label is defined from BMI; the model uses lifestyle factors only.
- **Preprocessing:** duplicates removed; yes/no and frequency answers mapped to integers (Sometimes 1, Frequently 2, Always 3); gender and transport mode integer-coded. No scaling, since all models are tree-based.
- **Validation:** 70:30 stratified train/test split (`random_state=42`), 5-fold stratified cross-validation on the training set.
- **Models:** Random Forest, XGBoost, Gradient Boosting, Decision Tree, and a majority-class baseline.

## Results

| Model | CV F1 (5-fold, mean ± std) | Test accuracy | Test F1 | Test ROC AUC |
|---|---|---|---|---|
| Majority baseline | 0 | 0.534 | 0 | 0.50 |
| **Random Forest** | **0.925 ± 0.015** | **0.927** | **0.921** | **0.970** |
| XGBoost | 0.925 ± 0.019 | 0.923 | 0.920 | 0.966 |
| Gradient Boosting | 0.872 ± 0.018 | 0.869 | 0.865 | 0.940 |
| Decision Tree | 0.877 ± 0.019 | 0.866 | 0.858 | 0.866 |

**Most important features** (permutation importance, Random Forest): age, family history of overweight, vegetable intake, number of main meals, eating between meals. Smoking and calorie monitoring add almost nothing.

## Limitations

About 77% of the records were generated synthetically by the dataset's authors (SMOTE). Near-copies can fall into both training and test sets, so the scores are likely optimistic for a real population.

## How to run

```bash
pip install pandas scikit-learn xgboost matplotlib
# download the CSV from the UCI link above into this folder
jupyter notebook obesity_lifestyle_only.ipynb
```

Coursework project, Master of Data Science, University of Malaya (2024); updated 2026.
