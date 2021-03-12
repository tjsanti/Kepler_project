# Kepler Project
Trevor Santiago

## Classifying Exoplanets with Kepler Data

The goal of this project is to see how well we can predict whether a Kepler Object of Interest (KOI) is confirmed to be an exoplanet, or is a false positive. I am mainly concerned with getting the highest accuracy as possible, but also look at log-loss to see the confidence of the model.

### The Data

The dataset I used comes from [Kaggle](https://www.kaggle.com/nasa/kepler-exoplanet-search-results), but is originally from NASA. The target variable is `koi_pdisposition`, which has values `CONFIRMED` and `FALSE POSITIVE` and is fairly balanced. An extensive data dictionary is available from NASA [here](https://exoplanetarchive.ipac.caltech.edu/docs/API_kepcandidate_columns.html).

### Approach

Lucky enough, the dataset is fairly tidy already. There are quite a few columns that I decided were either unimportant or contained leakage through exploratory analysis and the data dictionary. These columns are discarded during each model fit with the help of Sci-kit Learn's `ColumnTransformer`. Each model fit takes advantage of their `Pipeline` and `ColumnTransformer` objects.

I began with a simple baseline model using `sklearn`'s `KneighborsClassifier`. I then explored some other simple models such as `Logistic Regression`, as well as ensembling techniques like bagging. Next I tried out some more robust models such as `RandomForestClassifier` in a random hyperparamater search.

Finally, I used the best estimator output from the `RandomizedSearchCV` to explore more model structures. The model that I ended up choosing to be my final model used this best estimator as a meta-learner in a `StackingClassifier`. 

### Results

The final model mentioned above achieved an accuracy of about 86% and a log-loss around 0.32. I do no think this result is the ground for replacing scientists at NASA, but I am happy with the performance. You can access and run my code here:

Note that due to the randomness throughout the notebook and modelling process, the results you see from running it may vary from those I mention.
