# Measuring machine learning performance

## Loss function

**Loss function**: measures the difference between prediction and reality, i.e. the accuracy of the model
* Remember: when training a model, we use an optimization algorithm to pick parameters that minimize the loss function
* The same loss function can be used to measure the model's performance against the test set
* In a way, minimax is a loss function!

What kinds of loss functions are there?
* Many! Some are better for [classification](https://scikit-learn.org/stable/modules/model_evaluation.html#classification-metrics) and some are better for [regression](https://scikit-learn.org/stable/modules/model_evaluation.html#regression-metrics).
* Common classification loss functions
  * [**ROC AUC**](https://en.wikipedia.org/wiki/Receiver_operating_characteristic)
  * [**confusion matrix**](https://en.wikipedia.org/wiki/Confusion_matrix)
  * [**log loss**](https://en.wikipedia.org/wiki/Loss_functions_for_classification#Logistic_loss)
* [Fernando-Delgado _et al._, 2014](http://jmlr.org/papers/volume15/delgado14a/delgado14a.pdf) primarily use **accuracy**: number of correct predictions divided by total number of predictions

## Cross-validation

Remember: labeled input data is randomly partitioned into training and test sets. The test data is used to validate the model.

Why?
* **Training error**: calculating the loss function on the training data
* **Test error**: calculating the loss function on the test data
* Training error only measures how well the model fits the training data
* Test error provides an estimate for how well the model will perform on new data, i.e. **generalizability**
* **Overfitting**: when a model fits the training data too closely and performs badly on test data

**Cross-validation**: partitioning labeled input data into training and test sets one or more times to assess generalizability
* **Holdout method**: doing this partition once
  * Easy to do
  * But sometimes measure of error will change dramatically if the data is partitioned differently or if the ratio of training to test data sizes changes
* [**Leave-one-out (LOO) cross-validation**](https://scikit-learn.org/stable/modules/cross_validation.html#leave-one-out-loo): 
  * Given _n_ data points in labeled input data, split so that there is one data point in the test set and the rest are in the training set
  * Repeat, taking out a different data point for the test set each time
  * Average the loss function calculation across the _n_ iterations
  * Exhaustive but computationally expensive
* [**k-fold cross-validation**](https://scikit-learn.org/stable/modules/cross_validation.html#k-fold):
  * Split labeled input data into _k_ equally sized subsamples so that one subsample is used for the test set and _k - 1_ subsamples are used for the training set
  * Repeat, taking out a different subsample for the test set each time
  * Average the loss function calculation across the _k_ iterations
  * Less comprehensive than leave-one-out but faster
  * [Fernando-Delgado _et al._, 2014](http://jmlr.org/papers/volume15/delgado14a/delgado14a.pdf) use 4-fold cross-validation to evaluate the classifiers
* See [Wikipedia](https://en.wikipedia.org/wiki/Cross-validation_(statistics)) and [`scikit-learn` documentation](https://scikit-learn.org/stable/modules/cross_validation.html#cross-validation-iterators) for more variations