# Data Science Excessive Absenteeism Estimator : Project Overview

## Presentation

In a society where productivity is key, I did a project in which we could predict who is most likely to be absent and so, take action before it happends.\
The goal is to know whether a person present certain characteristics preliminary of an absenteeism.

At the end, we would get an answer whether someone will probably be excessively absent or not :\
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
