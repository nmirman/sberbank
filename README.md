# sberbank

This is an analysis of real estate data hosted on [kaggle](https://www.kaggle.com/c/sberbank-russian-housing-market).  The goal is to predict real estate prices in Moscow, Russia during the period July 2015 to May 2016 using training data from 2011-2015.

The core analysis is summarized in [this jupyter notebook](Sberbank.ipynb).

### Dataset features

Property data includes:
   * Area (m^2)
   * Kitchen size (m^2)
   * Number of rooms
   * Floor of building
   * Maximum floor of building
   * Distance from landmarks in Moscow
   * Neighborhood in Moscow, and demographic features of the neighborhood

Macro-economic data includes:
   * Foreign currency exchange rates
   * Oil market data
   * GDP, and economic benchmarks of Russia
   

### Strategy

The statistical model employed here is based on extreme gradient boosting (http://xgboost.readthedocs.io/en/latest/).  The analysis is performed in several stages:
   * Data cleaning.  Remove typos and extreme outliers from the training dataset by looking at distributions of various features including the price, property area, and price per square meter.  Use interpolation to fill in missing values related to the property area.  Other missing values are handled automatically by XGBoost.
   * Geographic interpolation.  For each property, an interpolation technique is employed to determine typical values of the price per square meter in the vicinity of the property.  This interpolated value is then the most important feature in the XGBoost algorithm.
   * Statistical modeling and validation.  The training data is input into the XGBoost algorithm.  Hyperparameters are tuned using a 10-fold cross validation approach.
   * Results are output to a csv file.  During the exploratory analysis phase, the above steps were tested on an independent holdout set where the "true" result was known.  For the final result, all available training data is used for maximum statistical power.

### Result
This analysis gets a root-mean-square-log-error of 0.32 on the test data set provided on Kaggle.  For a more detailed evaluation of the model, see the jupyter notebook!
