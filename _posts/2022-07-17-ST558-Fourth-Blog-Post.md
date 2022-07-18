Machine Learning Methods
================
Josh Baber
7/17/2022

## Algorithms Covered

In our course, the machine learning algorithms we focused on were split
into two categories: regression models and tree-based methods. The
regression models we looked at were simple and multiple linear
regression as well as generalized linear models like Poisson regression
and logistic regression using the “logit” link. The tree-based methods
we covered involving regression and classification trees were bagging,
random forests, and boosting. We also covered the k Nearest Neighbor
method. Of these methods, I had only ever done linear and logistic
regression before, so it was super interesting to learn about tree-based
methods as they often have better prediction power.

## Random Forest Models

The most interesting algorithm to me was certainly the random forest.
They tend to have less prediction error than the other models, sometimes
boosting does better, and it is particularly useful for data with highly
correlated predictors or really strong predictors. Before I explain what
random forests do, I must first explain bagging. Bagging is short for
“Bootstrap Aggregation”, and is essentially an average of many tree
models. For a numeric response, we repeatedly fit each regression tree
model to a random sample of the data, then average the predictions made
by all of the models into a final prediction. For a categorical
response, we do the same process with classification trees, but choose a
final prediction to be the classification that has the majority of
predictions. There are other ways to choose the best final prediction
for categorical responses as well.

Random forests are essentially identical to bagging, except for one
major difference. Random forests use a different random subset of
predictors to make predictions for each individual tree model made. We
also must predetermine how many random predictors to subset to for each
tree. The motivation behind subsetting predictors is that there may be a
predictor or two that are really important, which leads to all of the
individual trees creating splits at the same point and thus creating
collinearity in our final prediction. If all of our models are similar
or the same, the final prediction is going to be pretty uninformative
and have high variance in prediction. If we wanted to have a more
complete idea of what predictors and splits to use, it is better to use
a random forest.

## Fitting a Random Forest Model Using the `caret` Package

The data set I am going to look at came from Kaggle. It is a data set of
768 patients who either do or do not have diabetes. There are eight
health-related predictors in the data set that we can use to predict
whether or not a person has diabetes. The link to the data set can be
found
[here.](%22https://www.kaggle.com/datasets/pushprajnamdev/diabetes-dataset%22)

First, I must read in the data using `read_csv()` from the `tidyverse`
package and read in the `caret` package.

``` r
# Read in packages and data
library(tidyverse)
library(caret)
diabetes <- read_csv("../../Data/diabetes.csv")
```

    ## Rows: 768 Columns: 9
    ## ── Column specification ───────────────────
    ## Delimiter: ","
    ## dbl (8): pregnancies, glucose, bloodpre...
    ## lgl (1): outcome
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

Next, I want to create a training/testing split of the data. I want to
train my model on a random subset that is 75% of the original data set,
then test the model to see how it does on the remaining 25%. To create
this split, I used the `createDataPartition()` function from the `caret`
package.

``` r
# Create random 75/25 split of indices
trainIndices <- createDataPartition(diabetes$outcome, p = 0.75, list = FALSE)
# The 75% indices go to the training set
diabetesTrain <- diabetes[trainIndices,]
# The remaining 25% indices go to the testing set
diabetesTest <- diabetes[-trainIndices,]
```

To fit the model on the training data, we use the `train()` function
from the `caret` package. There are quite a few things to note in the
code here. First, since the “outcome” variable is TRUE or FALSE, we must
coerce it to a factor variable with `as.factor()`. Next, we specify
`method = "rf"` to say we want to fit a random forest model here. The
random forest algorithm is going to create many classification trees
with random subsets of predictors and determine the final prediction
based on what the majority classification was for each observation . We
don’t know what the best number of predictors to randomly subset to is,
it may be just 1, it may be all 8, or it may be somewhere in between.
The number of subset predictors is called “m”. We can use the argument
`mtry = c(1:8)` in the `tuneGrid =` argument to try all m values from 1
to 8. We used 10-fold cross validation, repeated 3 times to determine
what the best value of m was. To do the cross validation, we use the
`trainControl` function. Lastly, it is important to standardize the
data, to do this we use the `preProcess` argument. I saved the model as
`diabetesForest`.

``` r
# Fit the random forest model on the training data
diabetesForest <- train(as.factor(outcome) ~ ., data = diabetesTrain, method = "rf",
                        # Perform 10 fold cross validation
                        trControl = trainControl(method = "repeatedcv", number = 10, repeats = 3),
                        # Standardize the data
                        preProcess = c("center", "scale"),
                        # Check all possible m values from 1 to 8
                        tuneGrid = expand.grid(mtry = c(1:8)))
```

Lastly, we want to see how the model does with predicting whether or not
someone has diabetes based on the other predictor variables. Since the
response is binary, we use a confusion matrix to see the proportion of
correct and incorrect predictions. To do this, we use the
`confusionMatrix()` function from the `caret` package to see how well
the model predicts the testing data set.

``` r
# Generate confusion matrix to assess model fit on testing data
confusionMatrix(data = as.factor(diabetesTest$outcome), reference = predict(diabetesForest, newdata = diabetesTest))
```

    ## Confusion Matrix and Statistics
    ## 
    ##           Reference
    ## Prediction FALSE TRUE
    ##      FALSE   110   15
    ##      TRUE     29   38
    ##                                           
    ##                Accuracy : 0.7708          
    ##                  95% CI : (0.7048, 0.8283)
    ##     No Information Rate : 0.724           
    ##     P-Value [Acc > NIR] : 0.08315         
    ##                                           
    ##                   Kappa : 0.4699          
    ##                                           
    ##  Mcnemar's Test P-Value : 0.05002         
    ##                                           
    ##             Sensitivity : 0.7914          
    ##             Specificity : 0.7170          
    ##          Pos Pred Value : 0.8800          
    ##          Neg Pred Value : 0.5672          
    ##              Prevalence : 0.7240          
    ##          Detection Rate : 0.5729          
    ##    Detection Prevalence : 0.6510          
    ##       Balanced Accuracy : 0.7542          
    ##                                           
    ##        'Positive' Class : FALSE           
    ## 

It appears the model predicted with about a 77.08% accuracy. The
no-information rate is 72.4%, meaning if we took the majority outcome
(which I believe is FALSE, or that a person does not have diabetes) and
guessed it for all data points, we would be correct 72.4% of the time.
Our prediction rate is only about 5% higher than that, so it appears to
need some work to be done or perhaps a different model fit. Regardless,
this is likely a better model for predicting than a single
classification tree, or a logistic regression.
