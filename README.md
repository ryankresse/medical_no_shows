# Medical Appointment No-Shows in Brazil

In this project I explored the [Kaggle no-show appointment](https://www.kaggle.com/joniarroba/noshowappointments/version/5) dataset, trying to learn what characteristics about a patient or an appointment might be predictive of whether the patient shows up.

## About the data

The dataset contains information about 111k medical appointments in Brazil, including patient demographic characteristics, geographic and temporal information, and whether the patient showed up. Unfortunately, as of this writing, the source of the data is confidential (as stated by the user who uploaded the data), so we don't know its exact source.


## Key findings

#### Predicting no-shows is difficult

Alas, the dependent variables in the dataset were not enough to train a model that was very good at predicting no-shows. 20% of appointments in the dataset resulted in no-shows, and my best model was about 81% accurate, meaning it was only 1% better than always predicting that the patient would show up. Most of the features were simply not strongly associated with whether the appointment would result in a no show.

I tried three models, logistic regression, a random forest and xgboost, and all yielded roughly the same results. As you can see in the confusion matrix below, the majority of the models' errors were false negaives -- predicting that the patient would show up when they did not. Decreasing the prediction threshold from .5 to .4 reduced these errors and improved accuracy, but only marignally.

![Confusion Matrix](imgs/confusion_matrix.png)

#### Appointments with low wait times are more likely to be attended

When there are less than around 10 days between when an appointment is scheduled and when it takes place, the patient is more likely to show up. This is particularly true for same-day appointments -- only 4% of them were no shows. This makes sense intuitively -- if you have a low wait time, you're less time to forget the appointment and perhaps you're more likely to have an acute illness.
![No show vs. wait time](https://raw.githubusercontent.com/ryankresse/medical_no_shows/blob/master/imgs/rate_vs_message.png)


#### Reminder messages slightly helpful in preventing no shows

Over the entire dataset (left plot below), reminder messages seem to be associated with a much higher rate of no shows. However, this is likely a result of the confounding effect of waiting time. No messages were sent for same day appointments, which patients were much more likely to show up for. So when you remove same day appointments (right plot), we see actually see a slightly lower rate of no shows when a messages were sent.

![No show vs. messages](https://raw.githubusercontent.com/ryankresse/projectname/medical_no_shows/imgs/rate_vs_message.png)

#### Number of previous no shows by a patient was associated with higher likelihood of a no show
This engineered feature makes sense -- if someone hasn't shown up before, they're probably more likely not to show up again. However, in around 90% of appointments the patient didn't have a previous no show, so this feature didn't help much in improving overall accuracy. If you were able to collect data over a longer time period to accumulate more of a 'track record' for patients, perhaps it could be more beneficial.


## Future Questions

#### Are  certain patients more/less likely to be influenced by a reminder message?
I quickly at glanced at no-show appointments where a reminder message was sent. I didn't notice anything different about those patients, but a deeper dive or more data could be helpful.

####  Could the content of a reminder message or when it's sent influence the no-show rate?
A study could investigating this question could help optimize resources.

#### If we gathered similar data in other counties, would the results be the same?


## Files
- EDA.ipynb: exploratory analysis
- random_forest_logistic_regression.ipynb: training a random forest and logistic regression model
- xgboost.ipynb: training an xgboost model








