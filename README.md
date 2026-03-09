# Kaggle-ML-Competition-2nd-Place-
Engineered an XGBoost model in Python, leveraging data cleaning, feature engineering, model selection, and hyperparameter tuning, securing 2nd place out of 70 students in a Kaggle competition at KAIST.

#### Hyperparameter tuning
I learned the meaning of hyperparameters and how to tune the parameter from the documentation of XGBoost pacakge (https://xgboost.readthedocs.io/en/latest/tutorials/param_tuning.html), this video (https://www.youtube.com/watch?v=AvWfL1Us3Kg) and this blog about optuna (https://forecastegy.com/posts/xgboost-hyperparameter-tuning-with-optuna/)

| Hyperparameter | Default - Range | If increase | Type |
|----------------|-----------------|-------------|------|
| max_depth | 6 - (2,30) (0 = no limit on depth)| overfit | control model complexity | 
| **min_child_weight** | 1 - (0.1,1) | regularize | control model complexity | 
| **clf__reg_alpha** | 0 - | L1 regularize | control model complexity | 
| **clf__reg_lambda** | 1 - | L2 regularize | control model complexity | 
| gamma | 1 - (0.1,1) | overfit | control model complexity | 
|  |  |  |
| subsample | 1- (0.5,1) | overfit, if reduce -> regularize | add randomness -> training robust to noise |
| colsample_bytree | 1 - (0.1,1) | overfit |add randomness -> training robust to noise |
| colsample_bylevel | 1 - (0.1,1) | overfit |add randomness -> training robust to noise |
|  |  |  |
| n_estimators | 100 - (10,1000) | lower training speed, better | sequencially boost next tree |
| learning_rate | 0.3 - (10,1000) | fast training speed / cannot converge | |
