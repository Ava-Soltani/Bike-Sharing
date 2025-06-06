# Report: Predict Bike Sharing Demand with AutoGluon Solution
#### Atieh Soltani

## Initial Training
### What did you realize when you tried to submit your predictions? What changes were needed to the output of the predictor to submit your results?
TODO: When I first tried to submit my predictions to Kaggle, the submission failed. After checking, I realized that some of the predicted values were negative — which doesn’t make sense for bike rentals. You obviously can’t have negative bikes rented!

To fix this, I looked at the predictions using .describe() and saw that the minimum value was below zero. So I added a quick step to set any negative predictions to zero before submitting:
predictions[predictions < 0] = 0
After that, the file was accepted by Kaggle, and I got my first score on the leaderboard.


### What was the top ranked model that performed?
TODO: The best-performing model turned out to be the one where I added extra features like hour and rush_hour, and also converted some columns like season and weather into categorical types. This model gave me the lowest RMSE score on Kaggle — 0.47535, which was significantly better than the initial model and even slightly better than the one with hyperparameter tuning.

It was a bit surprising that the hyperparameter-tuned model didn’t outperform the one with added features, but it shows how powerful simple, well-thought-out feature engineering can be.

## Exploratory data analysis and feature creation
### What did the exploratory analysis find and how did you add additional features?
TODO: During the exploratory analysis, I found that the datetime column contained useful information that wasn't being used directly. I extracted the hour from it and created a new feature called rush_hour to highlight common commuting times like mornings and evenings. I also changed the data types of season and weather from integers to categorical, since they represent distinct categories rather than continuous values. These changes helped the model better understand the data and improved the overall performance.
### How much better did your model preform after adding additional features and why do you think that is?
TODO: After adding additional features, the model's performance improved significantly. The Kaggle score dropped from 1.77548 with the initial model to 0.47535 after feature engineering. This big improvement likely happened because the new features — like hour, rush_hour, and the categorical versions of season and weather — gave the model more meaningful context about when and under what conditions bikes were rented. These features helped the model make more accurate predictions by capturing patterns that weren’t clear in the raw data alone.

## Hyper parameter tuning
### How much better did your model preform after trying different hyper parameters?
TODO: After tuning hyperparameters, the model's performance slightly decreased compared to the version with added features. The Kaggle score went from 0.47535 (with added features) to 0.49167 (with hyperparameter tuning). This shows that while tuning can help in some cases, it didn’t lead to further improvement here, possibly because the model was already well-optimized with the added features, and the tuning introduced unnecessary complexity or overfitting.

### If you were given more time with this dataset, where do you think you would spend more time?
TODO: If I had more time with this dataset, I would focus on deeper feature engineering. For example, I’d explore creating interaction features between weather and time, or look at trends across different days of the week and holidays more closely. I’d also experiment with more advanced hyperparameter tuning strategies or custom model ensembling. Lastly, I’d analyze the residuals (errors) to see where the model is struggling most, like under certain weather conditions or times of day to guide further improvements.

### Create a table with the models you ran, the hyperparameters modified, and the kaggle score.
|model|hpo1|hpo2|hpo3|score|
|--|--|--|--|--|
|initial|None|None|None|	1.77548|
|add_features|hour|rush hour|Season/Weather|0.47535|
|hpo|num_trials=10|searcher=random|time_limit=600|0.49167|

### Create a line plot showing the top model score for the three (or more) training runs during the project.

TODO: <img width="717" alt="Autoglun Vallidation RMSE" src="https://github.com/user-attachments/assets/b9c6f39e-ad25-424d-9f52-c3dff6793977" />


### Create a line plot showing the top kaggle score for the three (or more) prediction submissions during the project.

TODO:  <img width="752" alt="Kaggle Public Leaderboard RMSE" src="https://github.com/user-attachments/assets/9517a2d1-5abe-422c-a185-5121ae17b75b" />


## Summary
TODO: In this project, I tackled the challenge of predicting how many people would rent bikes on a given day using the Bike Sharing Demand dataset from Kaggle. I used AutoGluon, an AutoML library, to train and improve models step by step.

I started with a basic model using the raw dataset. While it worked, the predictions weren’t great; the initial Kaggle score was 1.77548. From there, I explored the data and added new features like the hour of the day and a rush hour flag, and I also converted some numerical columns (like season and weather) into categories so the model could treat them more appropriately. These small changes made a big difference — the score improved to 0.47535.

To push things further, I tried tuning the model’s hyperparameters using randomized search. The score didn’t improve dramatically (it landed at 0.49167), but it was still a great opportunity to understand how tuning affects performance.

Along the way, I submitted multiple models to Kaggle, created helpful visualizations, and made sure the predictions were clean and valid. This project gave me hands-on experience with AutoML, feature engineering, and iterative model improvement, all while solving a real-world problem.
