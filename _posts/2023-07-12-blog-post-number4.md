Blog 4: Reflections on Machine Learning
================
Michael Bradshaw
2023-07-13

## Machine Learning Methods:

One modeling technique that I had heard about but didn’t know much about
was the Random Forest algorithm. Random Forest is an ensemble learning
technique that uses decision tress (similar to a flow chart) to make
predictions. The idea is to construct an ensemble of decision trees by
training each tree on a random subset of the data and a random subset of
the predictors. Each individual tree independently make predictions, but
the final prediction is determined by aggregating the results. Random
Forest techniques are beneficial because they can handle a large number
of predictors, and they are able to handle non-linear relationships and
interactions between variables.

``` r
# Load the caret package
library(caret)

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

We just finished our section on machine learning (woot). What method did
you find most interesting? Write a little about the method, fit the
model on some data, and provide any relevant output.
