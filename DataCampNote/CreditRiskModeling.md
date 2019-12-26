* Check df dataTypes
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
