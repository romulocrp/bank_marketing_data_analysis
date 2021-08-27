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

## Exploratory Data Analysis
### Descriptive analytics
   First I will consider the outlier treated data, which means that I’m going to consider the fewer entries than the available from the dataset, in exchange I’m going to have more normalized and well-distributed data across the variables.
   
   The first results aggregated are from a population characterization, using descriptive statistics, is possible to understand what is the most common characteristics of the clients f the bank, first the average numeric analysis:
- Age: 40.37
- Balance: 606.67
- Duration: 205.36
- Campaign: 2.19

    Other numeric values are 0 or date-related, which will be discussed later. Most of the population are encountered below these values:
- Age: 48
- Balance: 920
- Duration: 277
- Campaign: 3

    The relevant information here is that most people are below 48 years, don’t have more than 920 euros in the account, talked less than 5 minutes on the phone, and were contacted 3 times or less. The min and max values are, respectively:
- Age: 18, 70
- Balance: -1944, 3462
- Duration: 0, 643
- Campaign: 1, 6

    Here lies more relevant information, all the entries are above 18 years, negative balance means people in debt, the duration is at a max of almost 11 minutes of contact duration, and people were called at a max of 6 times during the time of the campaign.
### Frequency Distributions
   The categorical values can be analyzed by frequency distributions graphs, each value will be displayed below according to the most frequent to the least frequent:
- Job: Blue-collar, Management, Technician, Administrative, Services, Entrepreneur, Self-employed, Unemployed, Housemaid, Student, Unknown.
- Marital: Married, Single, Divorced.
- Education: Secondary, Tertiary, Primary, Unknown.
- Default: No, Yes.
- Housing: Yes, No.
- Loan: No, Yes.
- Contact: Cellphone, Unknown, Telephone.
- Poutcome: Unknown.

    So, building the persona target for this campaign, given this dataset is, Married, work either in a blue-collar or management job, has a secondary education, has a housing loan not defaulted yet, was contacted by cellphone and, since was never contacted for any other campaign, don’t have previous information if it is prone to accept the offer.
### Date related information
   In order to recover date related information, it was necessary to craft a variable that stores this information, from the website where the data set is available, there is an important piece of information, all the entries are in chronological order, which means that the first entry is in 2008 and the last is in 2010.
   
   First, a year column was put in place to organize the years, and then day, month, and year were used to build a column called “lc-date” it is about the last contact date the campaign had with the client.
   
   Counting the entries in the “y” feature by date would give the periods of activity of the campaign over the year, we have an immense spike in the beginning, from May 1, 2008, to August 31, 2008, where 18,330 entries were put in place, the other spike was between November 1, 2008, to June 30, 2009, where 8,370 entries were made.
### Response
   So is possible to check how many “yeses” and “nos” are in the dataset, the numbers are as follows:
- Yes: 1599
- No: 26594

   What does that mean? Well, at first is possible to state that it’s a high unbalanced dataset, the success rate of the campaign was 5.6%, given this result, the response frequency on the standard dataset was checked, the rate was 12.84%. This clearly states that after running the outlier treatment of the dataset, many yes responses were thrown out of the dataset.
   
Hence, the average client of the bank is not the best target to address with the campaign, there must be a better profile of client to reach.
### Success rate
   Considering the average results of a direct telephone campaign, this one was pretty average, accordingly with the Houston Chronicle, the average telemarketing campaign has a 12.95% success rate since this was the expected result, a less than half result to the average client means that the real target relies on the outliers.
### Profit
   So the average rate to a 1-year term deposit in Portugal is 1.76% a year, according to The Global Economy website, the minimum to open a term deposit can be as low as 250 euros. Usually, telemarketing campaigns don’t last so long, but a 2-month campaign can cost up to 10,000 euros. Using Insil telemarketing ROI calculator, the cost per buyer is 54.56 euros, for the first 4 months of the campaign, to regain 5 times more with minimum deposit, not counting the interest and period of time.
   
   Calculating the 2 year time the campaign was on, the total cost was 120,000 euros and the revenue was 1,322,250 euros, the profit was 1,202,250 euros, not counting the interest and minimum initial investment on the bank.
## Conclusion
   The average persona of this bank is not the best target for a term deposit telemarketing campaign, somehow the variables with outliers are related to a higher response rate. This is proven by the success rate on both cases, outlier treated dataset and not treated dataset, in its totality, the bank achieve average results for a telemarketing campaign, with a minimum profit of 1,202,250 euros for the entirety of the campaign.
## Next Steps
- Encode categorical values of the dataset
- Perform a multivariate analysis
- Search for correlations in the variables
- Incorporate new graphs on Streamlit application.
### Medium publications
   Also check out my publications on Medium about this app!
   
https://medium.com/analytics-vidhya/building-a-functional-dashboard-on-streamlit-bff831fdc2aa
