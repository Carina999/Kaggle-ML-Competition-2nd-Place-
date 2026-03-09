# Kaggle ML Competition (2nd place out of 70 students)
I engineered an XGBoost model in Python, leveraging data cleaning, feature engineering, model selection, and hyperparameter tuning, securing 2nd place out of 70 students in a Kaggle competition at KAIST.
- The complete code is in ML_code_Carina.ipynb

# XGBoost Hyperparameter tuning
I learned the meaning of hyperparameters and how to tune the parameters from the documentation of the XGBoost package (https://xgboost.readthedocs.io/en/latest/tutorials/param_tuning.html), this video (https://www.youtube.com/watch?v=AvWfL1Us3Kg) and this blog about optuna (https://forecastegy.com/posts/xgboost-hyperparameter-tuning-with-optuna/).

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


# Model Evaluation and Hyperparameters Tuning Methods
Tuning Methods: I used RepeatedStratifiedKFold to tune the C parameter in the multinomial logistic regression model, Optuna to tune the hyperparameters in the tree-based methods, and BayesSearchCV to tune the hyperparameters in XGBoost and SVM.  Among all of these methods, I found BayesSearchCV to be the easiest to implement because it allowed for efficient exploration of the hyperparameter space while automatically adjusting the search based on previous evaluations. This adaptive search capability streamlined the tuning process, requiring less manual intervention compared to other methods.          

Tuning Speed: The tuning speed for SVM using BayesSearchCV is much slower than that of XGBoost. For the boosting model, since it took me 1 hour to run 10 iterations using Optuna, I randomly selected some values for the hyperparameters and am reporting the results here. It turned out that if the `max_depth` is not too large, the model tends not to overfit, and the model performance is quite good.

Feature importance in tree-based models: In all tree-based methods, as indicated by the photo above. The feature **absences** consistently ranks first in the feature importance plot. This indicates that the absence or presence of certain features has a significant impact on the model's predictions. Additionally, the feature "Medu" consistently ranks at the very top in terms of importance. This suggests that the mother's education level plays a crucial role in determining the target variable in the dataset. 


| **Algorithm**      | **Best CV Accuracy** | **Train Accuracy** | **Test Accuracy** | **Public Score** | **Private Score** | **Hyperparameters**            |
|--------------------|----------------------|--------------------|-------------------|------------------|-------------------|-------------------------------|
| 1. Multinomial     | 0.384                | 0.3938             | 0.3934            | 0.42295          | 0.4               | C = 0.004                     |       
| 2.1 Classification tree| 0.3758           | 0.3759             | 0.3831            | 0.40983          | 0.378             | max-depth = 1 |
| 2.2 Bagging        | 0.3928               | 0.4292             |0.3814            | 0.3836           |0.35737            | max-depth = 5 |
| 2.3 Random Forest  | 0.3985               | 0.4221          | 0.42                 | 0.3738              |0.3607          | max-depth = 8, max-feature = 14 |
| 2.4 Boosting (no tuning)|                  | 0.5492           |0.4385         |    0.40625              | 0.42622           |  See model above|
| 2.5 XGBoost        | 0.3919               | 0.4038             |                   |0.42262           |0.42295            | See picture above             |
| 3. SVM             | 0.3821                |0.4113             |0.3811             |0.41967           |0.40327            |  C=1000000        |


# References        
1. FAMD. https://www.youtube.com/watch?v=Ollp2nSQCLY & https://maxhalford.github.io/prince/famd/
2. Ordinal regression: https://analyticsindiamag.com/a-complete-tutorial-on-ordinal-regression-in-python/
3. Encoding: https://www.analyticsvidhya.com/blog/2020/08/types-of-categorical-data-encoding/
4. MinMax vs Standardize: https://www.cnblogs.com/GouQ/p/11840653.html 
5. XGBoost: https://xgboost.readthedocs.io/en/latest/tutorials/param_tuning.html
6. XGBoost: https://www.youtube.com/watch?v=AvWfL1Us3Kg
7. Optuna: https://forecastegy.com/posts/xgboost-hyperparameter-tuning-with-optuna/
8. TPOTClassifier: https://towardsdatascience.com/tpot-automated-machine-learning-in-python-4c063b3e5de9 
