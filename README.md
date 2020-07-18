# Data Science Excessive Absenteeism Estimator : Project Overview

## Presentation

In a society where productivity is key, I did a project in which we could predict who is most likely to be absent and so, take action before it happends.\
The goal is to know whether a person present certain characteristics preliminary of an absenteeism.

At the end, we would get an answer whether someone will probably be excessively absent or not :
* **0:** will probably not be excessively absent.
* **1:** will probably be absent.

## Summary

* Created a tool that estimates possible excessive absenteeism with a score of 75% which would help preventing it.
* Used real world data.
* cleaned and made sense of the data.
* Engineered features to get the most out of the given data.
* Built a module for fast and easy integration.
* Used the predictions to find an indicator of future absenteeism and get insight from Tableau integration.

## Code and Resources Used

**Python Version:** 3.7\
**Packages:** numpy, pandas, pickle, sklearn.preprocessing: StandardScaler, sklearn.base: BaseEstimator/TransformerMixin\
**365DataScience course**

## Data Preprocessing

The given Data already was quite cleaned:
* No missing values.
* the nominal qualitative feature "Reason for Abscence" was already transformed using One-hot encoding.\
* The same for Education feature.\
(Reason for Abscence table) :
![reason for absenteeismpng](https://github.com/CaruzzoC/ds_absenteeism_proj/blob/master/image/reason%20for%20absenteeismpng.png)

What i did:
* Made four clusters for the "Reason for Abscence" feature: Reason_1, Reason_2, Reason_3, Reason_4
  * **Reason_1:** Various Diseases
  * **Reason_2:** Pregnancy and giving birth
  * **Reason_3:** Poisoning
  * **Reason_4:** Light diseases
* Made a column keeping the month, and a column for the day
* Made a column  for Education (not enough of each modality, so clustered in two groups : 1 with Education, 0 without)

## EDA

* To say if a certain amount of absenteeism hours is excessive or not, I took the median as an indicator. If someone have more absenteeism hours than the median, then it's excessive.
And so, i transformed the "Absenteeism Time in Hours" feature in a binarry feature :
  * **0:** Not excessively absent
  * **1:** Excessively absent
* Since it's the target, I made sure around half the data is excessively absent, and the other half is not.
* The features 'Day of the Week', 'Daily Work Load Average', 'Distance to Work' did not have a strong enough weight, so i dropped these features.
* The data range was sparse from a feature to an other, I then scaled the data excepted the binaries features.

## Model Building

Firstly, i chose to split my data with the following ratio :
 * **Training data:** 0.8
 * **Test data:** 0.2

The predicted value is binnary, I chose to use a LogisticRegression model to make the predictions. Once the model fit, i watched the coefficient and odds of each features to get a better understandment of their importance.
![coeff_odds_table](https://github.com/CaruzzoC/ds_absenteeism_proj/blob/master/image/coeff_odds_table.PNG)

## Productionization

In this step, I pickled the model i made, and also the custom scaler. This python module i made make the integration easier. With a new data, presenting the same shape as the first one, We fastly can get prediction. Using the absenteism_module methode, the "load_and_clean_data" method, and finally saving the result in a .csv file with the following method "predicted_outputs()".

## Tableau integration

As said in the presentation part, one of the goal is to point out an indicator of future excessive absenteeism.
the following graph have been made with this purpose.

![Age vs Probability](https://github.com/CaruzzoC/ds_absenteeism_proj/blob/master/tableau_graph/Age%20vs%20Probability.png)
This first graph shows that the age doesnt seem to be an indicator. The tendance is constant.

![Reason vs Probability](https://github.com/CaruzzoC/ds_absenteeism_proj/blob/master/tableau_graph/Reason%20vs%20Probability.png)
In this graph, the Reason_2 features have been deleted because none of the individu from the data have been excessively absent with the Reason_2. It doesnt give any insight.
Else, we have the three other different reason side by side :
  * **Reason_1:** The various diseases seem to have a strong positive impact on the excessive absenteeism.
  * **Reason_3:** As we can guess, poisoning reason have also a positive impact. (but we doesnt have much data about it).
  * **Reason_4:** The fourth type of reason seem to have a negative impact ont the excessive absenteeism.
The first reason if we check the table is about "serious diseases" (not to be discriminant). We can easly understand why someone would be excessively absent due to this condition.
The third reason is something we can classify as positive reason, but we should get more data about it to make it as a clear indicator.
The fourth reason is about light diseas and medical appointment. Someone being sick from time to time is not an indicator of excessive absenteeism.

![Transportation Expense and children](https://github.com/CaruzzoC/ds_absenteeism_proj/blob/master/tableau_graph/Transportation%20Expense%20and%20Children%20.png)
The transportation expense does not seem to have a direct link with the absenteesim. But from the graph, we can assume that children is an indicator of excessive absenteeism. (with one and more children, the tendance is positive, without children the tendance is negative).

![Pets vs Probability](https://github.com/CaruzzoC/ds_absenteeism_proj/blob/master/tableau_graph/Pets%20vs%20Probability.png)
Apparently having pets is a negative indicator of absenteeism. Maybe people who have pets and work have someone being able to take care of them while they are at work.

![Education vs Probability](https://github.com/CaruzzoC/ds_absenteeism_proj/blob/master/tableau_graph/Education%20vs%20Probability.png)
People with any kind of education seem to have lower probability to be excessively absent.

![Body Mass Index and Reasons](https://github.com/CaruzzoC/ds_absenteeism_proj/blob/master/tableau_graph/Body%20Mass%20Index%20and%20Reasons.png)
