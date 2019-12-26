* Check df dataTypes
```py
df.dypes
```
* Check loan_amount distribution
```py
n, bins, patches = plt.hist(x=cr_loan['loan_amnt'], bins='auto', color='blue',alpha=0.7, rwidth=0.85)
plt.xlabel("Loan Amount")
plt.show()
```
* Plot a scatter plot of income against age
```py
plt.scatter(cr_loan['person_income'], cr_loan['person_age'],c='blue', alpha=0.5)
plt.xlabel('Personal Income')
plt.ylabel('Person Age')
plt.show()
```
* cross tables, you get a high level view of selected columns + aggregation like a count or average. 
* For credit risk models, especially for probability of default, columns like ```person_emp_length``` and ```person_home_ownership``` are common to begin investigating.
```py
# Plot a scatter plot of income against age
plt.scatter(cr_loan['person_income'], cr_loan['person_age'],c='blue', alpha=0.5)
plt.xlabel('Personal Income')
plt.ylabel('Person Age')
plt.show()
```
* Create a cross table of the loan intent and status
```py
print(pd.crosstab(cr_loan['loan_intent'], cr_loan['loan_status'], margins = True))
```
* Create a cross table of home ownership, loan status, and grade
* Create a cross table of home ownership grouped by loan_status and loan_grade
* Two of the columns within cr_loan are grouped within []
```py
# 'person_home_ownership' = row, ['loan_status','loan_grade'] = stacked columns, value=normalCount
# 'loan_status' = above column, 'loan_grade' = below_column
print(pd.crosstab(cr_loan['person_home_ownership'],[cr_loan['loan_status'],cr_loan['loan_grade']]))
```
* Create a cross table of home ownership, loan status, and average percent income
```py
print(pd.crosstab(cr_loan['person_home_ownership'], cr_loan['loan_status'],
                  values=cr_loan['loan_percent_income'], aggfunc='mean'))
```
* Create a box plot of percentage income by loan status
```py
# loan_status = XAxis, 0 and 1, loan_percent_income = yAxis
cr_loan.boxplot(column = ['loan_percent_income'], by = 'loan_status')
plt.title('Average Percent Income by Loan Status')
plt.suptitle('')
plt.show()
```
---
### Detecting Outliers
```py
# Use crosstab
print(pd.crosstab(cr_loan['loan_status'],cr_loan['person_home_ownership'],
                  values=cr_loan['person_emp_length'], aggfunc='max'))
```
* Choose index of toBeDeleted rows
```py
# Create an array of indices where employment length is greater than 60
indices = cr_loan[cr_loan['person_emp_length'] > 60].index
```
* Drop rows based on indices
```py
# Drop the records from the data based on the indices and create a new dataframe
cr_loan_new = cr_loan.drop(indices)
```
