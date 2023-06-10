# Report: Predict Bike Sharing Demand with AutoGluon Solution
#### Connor Hunszinger

## Initial Training
### What did you realize when you tried to submit your predictions? What changes were needed to the output of the predictor to submit your results?
I did not have any issues. The notebook suggested that having any negative values will cause Kaggle to reject the submission, but luckily all my values were positive.

The notebook did not automatically submit the score: I had to download the .csv and submit it manually.

### What was the top ranked model that performed?
Strangley, my top-ranked model (lowest score) was actually the initial one. I think that adding a feature (hour of the day) without deleting the string value for datetime may have been the source of the issue. I should have added features for all parts of the datetime string, and then removed the datetime string.

## Exploratory data analysis and feature creation
### What did the exploratory analysis find and how did you add additional features?
The exploratory analysis revealed that many of the features are actually discrete values. Season and Weather should both be categories, so I changed that.

I also added the hour of the day, which i extracted from the string for DateTime.

### How much better did your model preform after adding additional features and why do you think that is?
The model score improved slightly - from -53.0 to -52.7. Unfortunately, I did not see much improvement. The kaggle score actually got slightly worse, as it went from 1.798 to 1.799.

I think that adding the new feature (hours) without removing the old one (datetime) was causing problems.

## Hyper parameter tuning
### How much better did your model perform after trying different hyper parameters?
The model score improved from -52.7 ro -51.1. Again, the kaggle score got slightly worse. I think this may be due to overfitting: I doubled the training time, as the documentation I read said that the hyperparameters I changed would increase training time. I may have increased it too much.

### If you were given more time with this dataset, where do you think you would spend more time?
I would add many more features for the time and date, and remove the datetime strings. I would also try representing the time in a different ways: for example, seperating into Day, Month, Year, or just have a category thats like "number of days since Jan 1 2000". The data would be the same, but I would be interested to see how the model reacts to it being presented differently.

### Create a table with the models you ran, the hyperparameters modified, and the kaggle score.
|model|time limit|num_stack_levels|num_bag_folds|num_bag_sets|score|
|--|--|--|--|--|--|
|initial|600|0|0|1|1.79841|
|add_features|600|0|0|1|1.79981|
|hpo|1200|1|8|2|1.82748|

### Create a line plot showing the top model score for the three (or more) training runs during the project.

TODO: Replace the image below with your own.

![model_train_score.png](img/model_train_score.png)

### Create a line plot showing the top kaggle score for the three (or more) prediction submissions during the project.

TODO: Replace the image below with your own.

![model_test_score.png](img/model_test_score.png)

## Summary
Adding features and tuning hyperparameters are useful tools in improving a model. However, if not used properly, they can also make the model worse. 

## Extra
I tried a few different options for hyperparameters (adjusting the same ones as above - just with different numbers) and got slightly better results. The table for those is shown below.

|model|time limit|num_stack_levels|num_bag_folds|num_bag_sets|score|
|--|--|--|--|--|--|
|hpo1|600|1|8|1|1.79337|
|hpo2|600|1|8|2|1.79796|
|hpo3|600|1|3|1|1.78532|
