# Regression
## Linear regression
- Simple case: 2 variables;
- Linear equation: y = mx + b;
- Estimation of parameters:
    - The estimation for m should be significantly different from 0, otherwise there is no meaningful dependency between x and y;
    - The estimation for b may or may not be significantly different from zero.
- Assume errors are independently and identically distributed, with constant variance.

## Evaluation of regression models:
### Prediction:
- Given the value of x, the model estimates the value of y;
- The estimate has an error equivalent to y' - y (y is the real value, y' is the prediction);

### Analysis of evaluation measures:
- Mean error: do NOT use;
- Mean absolute error: estimates "typical" error;
- Mean squared error: assigns more weight to larger errors, but that means it may be dominated by a few cases;
- Values depend on the scale of the target variable.

### Baseline: trivial model:
- Trivial model is assuming the mean value for every instance;
- Regression is only useful if its error is lower than the one obtained with the trivial prediction.

## Other algorithms:
### Nearest neighbour algorithm for regression:
- Find KNN, just like for classification;
- Predict the average of their target values, instead of majority voting.

### Decision trees for regression:
- Train: splitting criterion based on the sum of variances, instead of gini or entropy;
- Prediction: average of targets in the leaf, instead of majority voting;
- Variants: model trees (using MLR or KNN in the leaves instead of the average), MARS (multivariate adaptive regression splines).

### Neural networks for regression:
- Single output node, with predicted y as score;
- Continuous activation function (e.g. sigmoid).

### SVM for regression:
- Margin: minimise the tube "around" the data, instead of maximising the distance to closest examples from each class;

## Bias vs. variance
Bias: type of model an algorithm is able to learn given the set of training data; related to hypothesis language (e.g. linear vs. quadratic).

Variance: variation in model an algorithm is able to learn given different training data (i.e. small changes).

Bias-Variance trade-off: low bias implies high variance and vice-versa; find a model with a good trade-off (not too complex but with good predictive power).

### [< Go back](/README.md)