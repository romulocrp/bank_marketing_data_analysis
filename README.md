# Bank Telemarketing Data Analysis

## Business Problem

  Given this information by the bank how succesful was the campaign? What were the tops and bottoms of the capaign? The clients were contacted via phone calls and to achieve success in the campaign some were contacted more than once.

## Solution Strategy
  This project envisions running an exploratory data analysis on the dataset and then building a web page to display all the results and relevant information about the campaign.
  The step-by-step is given by:
- Download dataset
- Perform a sanity check
- Perform descriptive statistics
- Generate insight about the client base
- Build a dashboard using Streamlit framework

## Dataset
  The dataset used was provided by UCI Machine Learning Repository, under the name “Bank Marketing Data Set” via this link: https://archive.ics.uci.edu/ml/datasets/Bank+Marketing.
The variables are:
- age (numeric)
- job : type of job (categorical: 'admin.','blue-collar','entrepreneur','housemaid','management','retired','self-employed,'services','student','technician','unemployed','unknown')
- marital : marital status (categorical: 'divorced','married','single','unknown'; note: 'divorced' means divorced or widowed)
- education (categorical): 'basic.4y','basic.6y','basic.9y','high.school','illiterate','professional.course','university.degree','unknown'
- default: has credit in default? (categorical): 'no','yes','unknown'
- housing: has housing loan? (categorical): 'no','yes','unknown'
- loan: has personal loan? (categorical: 'no','yes','unknown')
- contact: contact communication type (categorical: 'cellular','telephone')
- month: last contact month of year (categorical: 'jan', 'feb', 'mar', ..., 'nov', 'dec')
- day_of_week: last contact day of the week (categorical: 'mon','tue','wed','thu','fri')
- duration: last contact duration, in seconds (numeric). Important note: this attribute highly affects the output target (e.g., if duration=0 then y='no'). Yet, the duration is not known before a call is performed. Also, after the end of the call y is obviously known. Thus, this input should only be included for benchmark purposes and should be discarded if the intention is to have a realistic predictive model.
- campaign: number of contacts performed during this campaign and for this client (numeric): includes the last contact
- pdays: number of days that passed by after the client was last contacted from a previous campaign (numeric): 0 means client was not previously contacted
- previous: number of contacts performed before this campaign and for this client (numeric)
- poutcome: outcome of the previous marketing campaign (categorical): 'failure', ‘nonexistent', ‘success'

## Sanity check
  No missing values were found in the dataset nor values out of the pattern proposed in each feature. Dataset has a shape of 41188 rows and 18 columns.
  Another test was tried out outlier detection, and a lot of outliers were detected using IQR rule of 1.5, with this approach it was clear to point out that the variables pdays and previous are normalized only to people that were never contacted before by the bank for a marketing campaign.
  For the campaign, duration and balance, they showed a large number of outliers detected, this result means that the populations of these features are highly skewed, since most outliers are concentrated in higher values, the skew is to the right. Age feature also shows a skew, far less pronunciation than the other three features.
  Given these results, is safe to say that to know the average client of the bank is required to consider all of the above-mentioned results, for this, new datasets were derived from the original to perform descriptive analytics.

