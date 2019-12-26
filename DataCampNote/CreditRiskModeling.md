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
* Create the similar table using min, max
```py
# Create the cross table from earlier and include minimum employment length
print(pd.crosstab(cr_loan_new['loan_status'],cr_loan_new['person_home_ownership'],
            values=cr_loan_new['person_emp_length'], aggfunc=['min','max']))
```
* Create the scatter plot for age and amount
```py
plt.scatter(cr_loan['person_age'], cr_loan['loan_amnt'], c='blue', alpha=0.5)
plt.xlabel("Person Age")
plt.ylabel("Loan Amount")
plt.show()
```
* Use Pandas to drop the record from the data frame and create a new one
```py
cr_loan_new = cr_loan.drop(cr_loan[cr_loan['person_age'] > 100].index)
# Create a scatter plot of age and interest rate
colors = ["blue","red"]
# Draw scatter plot from 'person_age', 'loan_int_rate' with different color of plot based on different status of 'loan_status'
plt.scatter(cr_loan_new['person_age'], cr_loan_new['loan_int_rate'], 
            c = cr_loan_new['loan_status'],
            cmap = matplotlib.colors.ListedColormap(colors),
            alpha=0.5)
plt.xlabel("Person Age")
plt.ylabel("Loan Interest Rate")
plt.show()
```
---
### Handle Missing Data
* Print an array of columns with null values in any of those columns
```py
print(cr_loan.columns[cr_loan.isnull().any()])
```
* Print top row of a series with nulls
```py
print(cr_loan[cr_loan['person_emp_length'].isnull()].head())
```
* Replace the null values with the median value for all employment lengths
```py
cr_loan['person_emp_length'].fillna((cr_loan['person_emp_length'].median()), inplace=True)
```
* Create a histogram of employment length
```py
n, bins, patches = plt.hist(cr_loan['person_emp_length'], bins='auto', color='blue')
plt.xlabel("Person Employment Length")
plt.show()
```
---
### Removing missing data
* Print the number of nulls
```py
print(cr_loan['loan_int_rate'].isnull().sum())
```
* Store the array on indices
```py
indices = cr_loan[cr_loan['loan_int_rate'].isnull()].index
```
* Save the new data without missing data
```py
cr_loan_clean = cr_loan.drop(indices)
```
* isnull(): to find missing value
* null records can be easily counted by sum()
* Show how many null in each column in a table format
```py
nullColumns = crLoan.columns[crLoan.isnull().any()]
crLoan[nullColumns].isnull().sum()
```
