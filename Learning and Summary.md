
1. Basic model performance ranks within expectations, newer and more sophiscated models tend to perform better.
2. Ensemble method can boost the accuracy by combining several different models.

3. AutoML technique provides a fast approach to train a high accuracy model without data pre-processing.</br>
  It does not score highest, but still can serve as a high benchmark for further model training and fine-tuning.</br>
  What suprised me is that pre-process the data with one-hot encoding actually drags dow the accuracy.

4. Most feature engineering does help much, due to small dataset and decent data quality.
  only feature engineering trick that works is taking logarithm of SalePrice, because the submission is evaluated on Root-Mean-Squared-Error (RMSE) between the logarithm of the predicted value and the logarithm of the observed SalePrice.

5. There are some models and techniques I didn't try but saw other people used, and they should boost the prediction accuracy:</br>
    Regresssion: ElasticNet, Ridge, etc.</br>
    Tree: CatBoost, etc.</br>
    Stacked Regressor</br>
    SVR, PCA</br>
    Feature Scaling</br>
    encoding: label,target, K-fold</br>

# Model Results

| Model Family   | Model                               | Price     | Feature Engineering | Encoding         | Score</br>(lower the better) |
|----------------|-------------------------------------|-----------|---------------------|------------------|-------------------------|
| Basic Model    | average of SalePrice                |           |                     |                  | 0.42672                 |
| Basic Model    | Lasso Regression                    |           |                     | one hot encoding | 0.14155                 |
| Basic Model    | Random Forest                       |           |                     | one hot encoding | 0.1497                  |
| Basic Model    | XGB                                 |           |                     | one hot encoding | 0.13466                 |
| Basic Model    | LGB                                 |           |                     | one hot encoding | 0.13188                 |
| Ensemble Model | Ensemble equal weight LGB,XGB,Lasso |           |                     |                  | 0.12448                 |
| Ensemble Model | 0.7 LGB, 0.2 XGB, 0.1 Lasso         |           |                     |                  | 0.12761                 |
| Ensemble Model | 0.5 LGB, 0.5 Lasso                  |           |                     |                  | 0.12415 :sparkles: Best |
| AutoML         | autogluon                           |           |                     |                  | 0.13209                 |
| AutoML         | autogluon                           | log_Price |                     | one hot encoding | 0.12852                 |
| AutoML         | autogluon                           | log_Price |                     |                  | 0.12614                 |
| Basic Model    | Lasso Regression                    | log_Price | Y                   | one hot encoding | 0.23122                 |
| Basic Model    | Random Forest                       | log_Price | Y                   | one hot encoding | 0.14559                 |
| Basic Model    | XGB                                 | log_Price | Y                   | one hot encoding | 0.12772                 |
| Basic Model    | LGB                                 | log_Price | Y                   | one hot encoding | 0.1293                  |
| Ensemble Model | 0.5 LGB, 0.5 XGB                    | log_Price | Y                   | one hot encoding | 0.12564                 |
| Ensemble Model | 0.5 LGB, 0.5 Lasso                  | log_Price | Y                   | one hot encoding | 0.16864                 |
| Ensemble Model | 0.7 LGB, 0.2 XGB, 0.1 Lasso         | log_Price | Y                   | one hot encoding | 0.1318                  |
| Ensemble Model | Ensemble equal weight LGB,XGB,Lasso | log_Price | Y                   | one hot encoding | 0.14942                 |
