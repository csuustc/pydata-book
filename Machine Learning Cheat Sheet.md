# Machine Learning Cheat Sheet

## Estimator API

1. Choose a class of model by importing the appropriate estimator class from Scikit-Learn.
2. Choose model hyperparameters by instantiating this class with desired values.
3. Arrange data into a features matrix and target vector following the discussion above.
4. Fit the model to your data by calling the ``fit()`` method of the model instance.
5. Apply the Model to new data:
   - For supervised learning, often we predict labels for unknown data using the ``predict()`` method.
   - For unsupervised learning, we often transform or infer properties of the data using the ``transform()`` or ``predict()`` method.

## Model Validation

### Holdout Sets

```python
# split the data with 50% in each set
from sklearn.model_selection import train_test_split
X_train, X_test, y_train, y_test = train_test_split(X, y, random_state=0(seed),
                                                    train_size = 0.5)
model.fit(X_train, y_train)
y_model = model.predict(X_test)
# evaluation
from sklearn.metrics import accuracy_score
accuracy_score(y_test, y_model)
```

### Cross-Validation

```python
# K-fold
from sklearn.model_selection import cross_val_score
cross_val_score(model, X, y, cv=5)
# LOOCV
from sklearn.model_selection import LeaveOneOut
cross_val_score(model, X, y, cv=LeaveOneOut())
# Validation Curve
from sklearn.model_selection import validation_curve
validation_curve(model, X, y, param_name, param_range, cv)
```

### Learning Curve

```python
from sklearn.model_selection import learning_curve
N, train_lc, val_lc = validation_curve(model, X, y, train_sizes, cv)
```

## Naive Bayes Classification



