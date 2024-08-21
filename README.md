# Bank-Marketing-Analysis: 
Citation of dataset: [Moro et al., 2011] S. Moro, R. Laureano and P. Cortez. Using Data Mining for Bank Direct Marketing: An Application of the CRISP-DM Methodology. 
## The dataset represents data collected from the direct marketing campaign of a bank from May 2008 to Nov 2010. The goals of this analysis are to provide the best classifier model and associated business insights into targetted marketing demographics.
## Dataset Attributes

1. **age**: numeric
2. **job**: type of job (categorical: "admin.","unknown","unemployed","management","housemaid","entrepreneur","student", "blue-collar","self-employed","retired","technician","services")
3. **marital**: marital status (categorical: "married","divorced","single"; note: "divorced" means divorced or widowed)
4. **education**: (categorical: "unknown","secondary","primary","tertiary")
5. **default**: has credit in default? (binary: "yes","no")
6. **balance**: average yearly balance, in euros (numeric)
7. **housing**: has housing loan? (binary: "yes","no")
8. **loan**: has personal loan? (binary: "yes","no")

## Related with the last contact of the current campaign:
9. **contact**: contact communication type (categorical: "unknown","telephone","cellular")
10. **day**: last contact day of the month (numeric)
11. **month**: last contact month of year (categorical: "jan", "feb", "mar", ..., "nov", "dec")
12. **duration**: last contact duration, in seconds (numeric)

## Other attributes:
13. **campaign**: number of contacts performed during this campaign and for this client (numeric, includes last contact)
14. **pdays**: number of days that passed by after the client was last contacted from a previous campaign (numeric, -1 means client was not previously contacted)
15. **previous**: number of contacts performed before this campaign and for this client (numeric)
16. **poutcome**: outcome of the previous marketing campaign (categorical: "unknown","other","failure","success")

## Output variable (desired target):
17. **y**: has the client subscribed a term deposit? (binary: "yes","no")

# Bottom line up front:
1. The data set is heavily biased towards the outcome of 'no' (11.6% yes, 88.4% no).
2. Of all four models, logisitic regression had the highest weighted average f1-score of 88%. Overall, all of the models we're fairly poor at predicting the 'yes' response.
3. KNN and SVC models both identified `poutcome = 'success'` as the most important feature to predict whether a person would execute a term deposit.
4. The Decision Tree model identified the duration of the contact as the most important feature, followed by `poutcome = 'success'`.
5. 18.49% of people who had previously accepted after a campaign initiated a term deposit, versus 11.68% acceptance from those who declined a previous campaign.
6. **Recommendations**: Bias marketing efforts towards older people with more education, who don't have personal loans, and maximize the frequency and duration of contact. I also recommend to target customers who have previously been receptive to marketing campaigns and placed term deposits before.
##### Summary table of model performance and hyperparameters
| Model                | Average Fit Time (seconds) | Train Score | Test Score | Optimal Hyperparameters                           |
|----------------------|----------------------------|-------------|------------|--------------------------------------------------|
| KNN                  | 0.030808210372924805       | 0.8966766202167662 | 0.8935087913303107 | {'n_neighbors': 30}                               |
| SVC                  | 18.33925051689148          | 0.8933864189338642 | 0.8907442220502045 | {'kernel': 'linear'}                              |
| Logistic Regression  | 0.08978357315063476        | 0.9012386640123866 | 0.8976003538648678 | {'C': 1, 'penalty': 'l2', 'solver': 'newton-cg'}  |
| Decision Tree        | 0.06227860450744629        | 0.9030911302809113 | 0.8952781156695787 | {'criterion': 'gini', 'max_depth': 4, 'min_samples_split': 2} |
##### Summary table of classification reports
| Model                | Precision (no) | Recall (no) | F1-Score (no) | Support (no) | Precision (yes) | Recall (yes) | F1-Score (yes) | Support (yes) | Accuracy | Macro Avg Precision | Macro Avg Recall | Macro Avg F1-Score | Weighted Avg Precision | Weighted Avg Recall | Weighted Avg F1-Score |
|----------------------|----------------|-------------|---------------|--------------|-----------------|--------------|----------------|---------------|----------|---------------------|------------------|--------------------|------------------------|---------------------|----------------------|
| KNN                  | 0.90           | 0.99        | 0.94          | 7952         | 0.68            | 0.22         | 0.33           | 1091          | 0.89     | 0.79                | 0.60             | 0.64               | 0.88                   | 0.89                | 0.87                 |
| SVC                  | 0.90           | 0.99        | 0.94          | 7952         | 0.67            | 0.19         | 0.29           | 1091          | 0.89     | 0.78                | 0.59             | 0.62               | 0.87                   | 0.89                | 0.86                 |
| Logistic Regression  | 0.91           | 0.98        | 0.94          | 7952         | 0.65            | 0.33         | 0.44           | 1091          | 0.90     | 0.78                | 0.65             | 0.69               | 0.88                   | 0.90                | 0.88                 |
| Decision Tree        | 0.91           | 0.97        | 0.94          | 7952         | 0.62            | 0.33         | 0.43           | 1091          | 0.90     | 0.77                | 0.65             | 0.69               | 0.88                   | 0.90                | 0.88                 |
### Concluding thoughts
#### All four models did well with predicting the majority class but poorly with the minority class. Using feature/permutation importance, we were able to extract some common features across all the models, such as poutcome = 'success'. Unfortunately, much of the poutcome data is unknown, so it would be valuable to get better data for this feature. Logistic regression is a suitable model for this dataset; it was slightly slower than KNN and DT but yielded the best recall score for ‘yes’.
