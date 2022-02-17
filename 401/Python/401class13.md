## Linear Regression

- Scikit-learn is a powerful Python module for machine learning. It contains functions for regression, calssification, clustering, model selection and dimensionality reduction.

## Exploring Boston Housing Data Set

- import required Python libraries into Ipython Notebook
- `import numpy as np`
- `import pandas as pd`
- `import scipy.stats as stats`
- `import matplotlib.pyplot as plot`
- `import sklearn`

- import data set and store it in a variable called boston.
- `from sklean.datasets import load_boston`
- `boston = load_bost()`

- The object boston is a dictionary, so you can explore the keys of this dic.
- `boston.keys()`
- ['data', 'feature_names', 'DESCR', 'target']
- Get the rows and column with `boston.data.shape`.
- Print names: `print boston.feature_names` 

## Convert boston.data into a pandas data frame

- `bos = pd.DataFrame(boston.data)`
- `bos.head()` 

## Scikit Learn

- Use a linear regression model and predict the Boston housing prices.
- Y = boston housing price(also called "targe" data in Python)
- X = all the other features(or independent variables)
- Drop price column and only use the parameters as the X values.
- `from sklearn.linear_model import LinearRegression`
- `X = bos.drop('PRICE', axis = 1)`
- Create the LinearRegression object: `lm = LinearRegression()`

### Important Function to keep in mind

- `lm.fit()` -> fits a linear model
- `lm.predict()` -> Predict Y using the linear model with estimated coefficients
- `lm.score()` -> Returns the coefficient of determination (R^2). A measure of how well ovserved outcomes are replicated by the mode, as the proportion of total variation of outcomes explained by the models.