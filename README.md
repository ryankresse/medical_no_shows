# Medical Appointment No-Shows in Brazil

In this project I explored the [Kaggle no-show appointment](https://www.kaggle.com/joniarroba/noshowappointments/version/5) dataset, trying to learn what characteristics about a patient or an appointment might be predictive of whether the patient shows up.

## About the data

The dataset contains information about 111k medical appointments in Brazil, including patient demographic characteristics, geographic and temporal information, and whether the patient showed up. Unfortunately, as of this writing, the source of the data is confidential (as stated by the user who uploaded the data), so we don't know its exact source.


## Key findings

#### Predicting no-shows is difficult

Alas, the dependent variables in the dataset were not enough to train a model that was very good at predicting no-shows. 20% of appointments in the dataset resulted in no-shows, and my best model was about 81% accurate, meaning it was only 1% better that always predicted that the patient would show up. Most of the features were simply not strongly associated with whether a patient showed up.

I tried three models, logistic regression, random forest and xgboost, and all yielded roughly the same results. As you can see in the confusion matrix below, the majority of the models' errors were false negaives -- predicting that the patient would show up when they did not. Decreasing the prediction threshold from .5 to .4 reduced these errors and improved accuracy, but only marignally.

![Confusion Matrix](https://raw.githubusercontent.com/ryankresse/projectname/master/confusion_matrix.png)

#### Appointments with low wait times are more likely to be attended

When there are less than around 10 days between when an appointment is scheduled and when it takes place, the patient is more likely to show up. This is particularly true for same-day appointments -- only 4% of them were no shows. This makes sense intuitively -- if you have a low wait time, you less time to forget the appointment and perhaps you're more likely to have an acute illness.

![No show vs. wait time](https://raw.githubusercontent.com/ryankresse/projectname/master/rate_vs_weight.png)
yankresse/projectname/master/rate_vs_weight.png)


#### Reminder messages slightly helpful in preventing no shows

This effect appears after removing same day appointments. If you include same day appointments (left plot below), messages seem to be associated with a much higher rate of no show. But this is likely due to the fact that no messages were sent for same day appointments, and that patients were much more likely to show up for them.

![No show vs. messages](https://raw.githubusercontent.com/ryankresse/projectname/master/rate_vs_message.png)



## Future Questions

#### Are there certain patients who are more/less likely to be influenced by a reminder message?
I quickly at glanced at no-show appointments where a reminder message was sent. I didn't notice anything different about those patients, but a deeper dive or more data could be helpful.

####  Could when a reminder message is sent or its content influence the no-show rate?
A study could investigating this question could help optimize resources.

#### If we gathered similar data in other counties, would the results be the same?











