# Classification of Obesity Levels Data Set

## Abstract
Utilizing a publically available data set, this project builds a classifier of obesity level between levels (Insufficient Weight, Normal Weight, Overweight Level I, Overweight Level II, Obesity Type I, Obesity Type II and Obesity Type III) based on eating habits and physical conditions of the individuals. 

## Dataset
UCI ML Repository: Estimation of obesity levels based on eating habits and physical condition Data Set found [here](https://archive.ics.uci.edu/ml/datasets/Estimation+of+obesity+levels+based+on+eating+habits+and+physical+condition+#). Based on the work found [here](https://www.sciencedirect.com/science/article/pii/S2352340919306985?via%3Dihub).

## Data Representation and Processing
The data is comprised of continous, binary, ordinal and nominal variables. The binary and ordinal variables were encoded accordingly with the nominal variables were one-hot encoded.  Following this EDA was performed to ensure that the resultant features where not correlated. Some of the mutually exclusive one-hot encoded variables where highly negatively correlated, but this is to be expected. Following this, the final feature values ('Gender', 'Age', 'Height', 'Weight', 'family_history_with_overweight', 'FAVC', 'FCVC', 'NCP','SMOKE', 'CH2O', 'SCC', 'FAF', 'TUE', 'ord_CAEC', 'ord_CALC', 'MTRANS_Automobile', 'MTRANS_Bike', 'MTRANS_Motorbike','MTRANS_Public_Transportation', 'MTRANS_Walking') were normalized to the range [0,1].  A stratified 20% of the original data set was held back as the test set.

## Model Derivation
Four models were optimized via grid search and 5-fold cross-validation: One vs Rest Logistic Regession, One vs Rest Support Vector Classifier, Random Forest, and XGBoost and scored on macro averaged F1 score.  The results were as follows:

| Model | Optimized Parameters | f1-score|
|-------|----------------------|---------|
| Logistic Regression | C: 10000.0, penalty: L2 | 0.774 |
| SVM | C: 1000.0 | 0.9134|
| Random Forest | max_depth: 64, n_estimators: 128 | 0.951 |
| XGBooost | colsample_bytree: 0.9, gamma: 0.4, max_depth: 4, min_child_weight: 4, subsample: 1.0 | 0.965 |

## Results
Scoring the random forest and XGBoost on the test set gives the following classification reports and confusion matricies:

#### Classification Report for Random Forest
![](https://github.com/jgalloway42/classification_of_obesity_levels/blob/main/obesity_rf_report.png)
<br>
![](https://github.com/jgalloway42/classification_of_obesity_levels/blob/main/obesity_rf_cfmatrix.png)

#### Classification Report for XGBoost
![](https://github.com/jgalloway42/classification_of_obesity_levels/blob/main/obesity_xgb_report.png)
<br>
![](https://github.com/jgalloway42/classification_of_obesity_levels/blob/main/obesity_xgboost_cfmatrix.png)

## Conclusion
Overall, both the random forest and XGBoost model performed very well with f1-scores over 95% in both cases. The random forest had trouble classifying Normal Weight and OverWeight I, whereas the XGBoost model had issues with Insufficient Weight, Normal Weight, Overweight Level I confusing them for Normal Weight. Future work may include training separate models to detect just those variables and then combining them via stacking to train a meta-model.

