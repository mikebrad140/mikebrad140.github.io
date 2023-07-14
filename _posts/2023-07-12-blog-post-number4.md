Blog 4: Reflections on Machine Learning
================
Michael Bradshaw
2023-07-14

## Machine Learning Methods: Random Forest

The Random Forest algorithm was a modeling technique that I had heard of
but had limited knowledge about. After watching the lectures, I now
understand that Random Forest is an ensemble learning technique that
uses decision tress (similar to a flow chart) to make predictions. The
idea is to construct an ensemble of decision trees by training each tree
on a random subset of the data and a random subset of the predictors.
Each individual tree independently make predictions, but the final
prediction is determined by aggregating the results. Random Forest
techniques are beneficial because they can handle a large number of
predictors, and they are able to handle non-linear relationships and
interactions between variables.

## Example Random Forest Model:

``` r
# Load the caret package
library(caret)
```

    ## Warning: package 'caret' was built under R version 4.2.3

    ## Loading required package: ggplot2

    ## Warning: package 'ggplot2' was built under R version 4.2.3

    ## Loading required package: lattice

    ## Warning: package 'lattice' was built under R version 4.2.3

``` r
# built in iris dataset
data(iris)

# Split the data into training and testing sets
set.seed(717)
train_indices <- createDataPartition(iris$Species, p = 0.7, list = FALSE)
train_data <- iris[train_indices, ]
test_data <- iris[-train_indices, ]

rf_model <- train(Species ~ ., data = train_data,
                  method = "rf",
                  trControl = trainControl(method = "repeatedcv", 
                                           number = 5, repeats = 3),
                  tuneGrid = data.frame(mtry = 1:4))


rf_predictions <- predict(rf_model, newdata = test_data)

# Create confusion matrices for each model
rf_cm <- confusionMatrix(rf_predictions, test_data$Species)

Accuracy<- rf_cm$overall["Accuracy"]
Accuracy 
```

    ##  Accuracy 
    ## 0.9333333

## Summary:

In this example, the Random Forest model was trained on the iris dataset
and achieved an accuracy of 0.9333 on the test data. AS such, the model
accurately predicted the species of the iris flowers in the test set
93.33% of the time.
