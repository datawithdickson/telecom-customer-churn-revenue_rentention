# Telecom Customer Churn & Revenue Retention Analysis

![Project Cover](https://github.com/datawithdickson/telecom-customer-churn-revenue_rentention/blob/main/global-network-connectivity-modern-city-skyline-sunset.jpg)

## Project Components

### 1. Python
Python was used for data loading, cleaning, exploratory data analysis, statistical analysis, visualisation and answering business questions.

**Libraries used:**
- Pandas
- NumPy
- Matplotlib
- Seaborn

### 2. Power BI
Power BI was used to develop an interactive dashboard for monitoring customer churn, retention and revenue performance.

### Power BI Dashboard 

- [Dashboard preview](https://github.com/datawithdickson/telecom-customer-churn-revenue_rentention/blob/main/Dashboard/Dashboard.png)
- [Download the Power BI report](https://github.com/datawithdickson/telecom-customer-churn-revenue_rentention/blob/main/Dashboard/IBM%20telecom%20project.pbix)

## Overview 
This project analyses customer churn and revenue patterns using the IBM Telco Customer Churn dataset. The analysis explores customer demographics, account information, subscribed services, payment methods and billing behaviour to identify characteristics associated with customer churn.

## Objectives

- Import the required Python libraries and load the customer churn dataset.
- Explore the dataset structure, variables and summary statistics.
- Clean and prepare the data for analysis.
- Perform exploratory data analysis on customer demographics, accounts, services and billing.
- Investigate business questions related to customer churn, retention and revenue.
- Translate the findings into practical customer-retention recommendations.


## Dataset

The data for this project is sourced from the Kaggle dataset:

- **Dataset Link:** [IBM Telco Customer Churn](https://www.kaggle.com/blastchar/telco-customer-churn/notebooks?utm_source=chatgpt.com)

## Project Structure

The project was carried out in Jupyter Notebook through five main tasks, followed by exploratory data analysis and investigations into eleven business questions.

### Task 1: Importing Libraries 
The following Python libraries were imported for data manipulation, numerical operations and visualisation.

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

%matplotlib inline
```

### Task 2: Loading the Dataset

The dataset was loaded into a Pandas DataFrame for analysis.

```python
df = pd.read_csv('WA_Fn-UseC_-Telco-Customer-Churn.csv')
```

### Task 3: Initial Exploration

Initial exploration was performed to understand the dataset's structure, dimensions, data types, statistical characteristics and sample records.

**Operations performed:**
- Displayed the first five records using `df.head()`.
- Displayed the last five records using `df.tail()`.
- Checked dataset dimensions using `df.shape`.
- Inspected column names, non-null counts and data types using `df.info()`.
- Generated descriptive statistics using `df.describe()`.
```python
df.head()
df.tail()
df.shape
df.info()
df.describe()
```
The initial exploration identified 7,043 records and 21 columns.

### Task 4: Data Cleaning

Data cleaning was performed to identify and address missing values, duplicates, incorrect data types and inconsistent categorical values.

**1. Missing Values**

The initial null-value check did not identify missing values. Further investigation revealed 11 blank entries in the `TotalCharges` column, stored as whitespace.

These records had zero customer tenure, indicating newly joined customers who had not accumulated total charges.

The blank entries were converted into proper missing values, the column was converted to numeric format, and the missing accumulated charges were replaced with zero.

```python
# Identify blank values
(df['TotalCharges'].astype(str).str.strip() == '').sum()

# Convert whitespace into missing values
df['TotalCharges'] = df['TotalCharges'].replace(
    r'^\s*$', pd.NA, regex=True
)

# Convert TotalCharges to numeric
df['TotalCharges'] = pd.to_numeric(df['TotalCharges'])

# Replace missing accumulated charges with zero
df['TotalCharges'] = df['TotalCharges'].fillna(0)

# Verify missing values
df.isnull().sum()
```

**2. Duplicate Records**

Duplicate records were checked to determine whether the dataset contained repeated observations.

```python
df.duplicated().sum()
```

No duplicate records were found.

**3. Data Types**

Data types were inspected to ensure that numerical and categorical variables were appropriately represented.

```python
df.dtypes
```

The `TotalCharges` column was converted to `float64` during the cleaning process.

**4. Categorical Data Validation**

Value counts were examined for selected categorical variables to identify unexpected or inconsistent categories.

```python
df['gender'].value_counts()
df['Contract'].value_counts()
df['PaymentMethod'].value_counts()
df['InternetService'].value_counts()
df['Churn'].value_counts()
df['Partner'].value_counts()
df['Dependents'].value_counts()
```

### Task 5: Data Analysis

The analysis was divided into two sections:

- Section A: Exploratory Data Analysis (EDA)
- Section B: Business Questions

### Section A: Exploratory Data Analysis (EDA)

#### 1. Customer Demographics

Explored the distribution of customers according to:
- Gender
- Senior citizen status
- Partner status
- Dependent status

```python
df[['gender', 'SeniorCitizen', 'Partner', 'Dependents']].describe()

df['gender'].value_counts()
df['SeniorCitizen'].value_counts()
df['Partner'].value_counts()
df['Dependents'].value_counts()
```

#### 2. Customer Account Information

Examined customer account characteristics, including contract type, tenure and paperless billing.

```python
df['Contract'].value_counts()
df['tenure'].value_counts().sort_index()
df['PaperlessBilling'].value_counts()

df['tenure'].describe()
```

#### 3. Customer Services

Explored the distribution of customers across phone, internet and additional subscription services.

```python
df['PhoneService'].value_counts()
df['MultipleLines'].value_counts()
df['InternetService'].value_counts()

df['OnlineSecurity'].value_counts()
df['OnlineBackup'].value_counts()
df['DeviceProtection'].value_counts()
df['TechSupport'].value_counts()
df['StreamingTV'].value_counts()
df['StreamingMovies'].value_counts()
```

#### 4. Customer Billing and Revenue

Examined payment methods, monthly charges, accumulated charges and total monthly revenue.

```python
df['PaymentMethod'].value_counts()

df['MonthlyCharges'].describe()
df['TotalCharges'].describe()

# Total monthly revenue
df['MonthlyCharges'].sum()
```

#### 5. Customer Churn

Examined the distribution of churned and retained customers and calculated the overall churn rate.

```python
df['Churn'].value_counts()

# Churn percentage distribution
df['Churn'].value_counts(normalize=True) * 100

# Overall churn rate
churn_rate = (df['Churn'] == 'Yes').mean() * 100

print(f"Overall Customer Churn Rate: {churn_rate:.2f}%")
```

#### 6. Numerical Variables Overview

Examined the statistical characteristics and correlations of numerical variables.

```python
df[['SeniorCitizen', 'tenure',
    'MonthlyCharges', 'TotalCharges']].describe()

df[['SeniorCitizen', 'tenure',
    'MonthlyCharges', 'TotalCharges']].corr()
```

### Section B: Business Questions

The following business questions guided the detailed analysis.

#### Q1. What is the overall customer churn rate?

Calculated the proportion of customers who discontinued their subscriptions and visualised the churn distribution.

```python
churn_rate = (df['Churn'] == 'Yes').mean() * 100

print(f"Overall Customer Churn Rate: {churn_rate:.2f}%")

churn_counts = df['Churn'].value_counts()

plt.figure(figsize=(5, 5))
plt.pie(
    churn_counts,
    labels=churn_counts.index,
    autopct='%1.1f%%',
    startangle=90
)

plt.title('Customer Churn Distribution')
plt.show()
```

#### Q2. What is the company's total monthly revenue?

Calculated total monthly revenue by summing the monthly charges across all customers.

```python
monthly_revenue = df['MonthlyCharges'].sum()

print(f"Total Monthly Revenue: ${monthly_revenue:,.2f}")

sns.displot(data=df, x='MonthlyCharges', bins=30)

plt.title('Distribution of Monthly Charges')
plt.ylabel('Number of Customers')
plt.show()
```

#### Q3. Which customer segments have the highest churn rates?

Compared churn rates across demographic categories, including gender, senior citizen status, partner status and dependent status.

```python
demographic_columns = [
    'gender',
    'SeniorCitizen',
    'Partner',
    'Dependents'
]

for column in demographic_columns:
    churn_rate = df.groupby(column)['Churn'].apply(
        lambda x: (x == 'Yes').mean() * 100
    )

    print(f"\nChurn Rate by {column}:")
    print(churn_rate.round(2))
```

#### Q4. How does tenure influence customer churn?

Grouped customers into new, medium-term and long-term customers to examine how churn rates differ across tenure groups.

```python
df['TenureGroup'] = pd.cut(
    df['tenure'],
    bins=[-1, 12, 48, 72],
    labels=[
        'new_customers',
        'medium-term_customers',
        'long-term_customers'
    ]
)

churn_by_tenure = df.groupby(
    'TenureGroup',
    observed=False
)['Churn'].apply(
    lambda x: (x == 'Yes').mean() * 100
)

print(churn_by_tenure.round(2))
```

#### Q5. Which contract types experience the highest churn?

Calculated churn rates across month-to-month, one-year and two-year contracts.

```python
churn_by_contract = df.groupby('Contract')['Churn'].apply(
    lambda x: (x == 'Yes').mean() * 100
)

print(churn_by_contract.round(2))
```

#### Q6. Does payment method relate to customer churn?

Compared churn rates across the four payment methods.

```python
churn_by_payment = df.groupby('PaymentMethod')['Churn'].apply(
    lambda x: (x == 'Yes').mean() * 100
)

print(churn_by_payment.round(2))

plt.figure(figsize=(9, 6))

sns.barplot(
    x=churn_by_payment.index,
    y=churn_by_payment.values,
    width=0.4
)

plt.title('Customer Churn Rate by Payment Method')
plt.xlabel('Payment Method')
plt.ylabel('Churn Rate (%)')

plt.show()
```

#### Q7. Which customer segments generate the highest revenue?

Compared total monthly revenue across demographic groups.

```python
# Revenue by gender
revenue_by_gender = df.groupby('gender')['MonthlyCharges'].sum()

# Revenue by senior citizen status
revenue_by_senior_citizen = df.groupby(
    'SeniorCitizen'
)['MonthlyCharges'].sum()

# Revenue by partner status
revenue_by_partner = df.groupby('Partner')['MonthlyCharges'].sum()

# Revenue by dependent status
revenue_by_dependents = df.groupby(
    'Dependents'
)['MonthlyCharges'].sum()

print(revenue_by_gender)
print(revenue_by_senior_citizen)
print(revenue_by_partner)
print(revenue_by_dependents)
```

#### Q8. How does average monthly spending differ between churned and retained customers?

Calculated and compared average monthly charges according to customer churn status.

```python
avg_spending = df.groupby('Churn')['MonthlyCharges'].mean()

print(avg_spending.round(2))

plt.figure(figsize=(5, 4))

sns.barplot(
    x=avg_spending.index,
    y=avg_spending.values,
    width=0.4
)

plt.title('Average Monthly Charges by Churn Status')
plt.xlabel('Customer Churn')
plt.ylabel('Average Monthly Charges ($)')

plt.show()
```

#### Q9. Does having additional services relate to customer retention?

Investigated churn rates among customers with different additional services, including online security, online backup, device protection, tech support, streaming TV and streaming movies.

```python
service_columns = [
    'OnlineSecurity',
    'OnlineBackup',
    'DeviceProtection',
    'TechSupport',
    'StreamingTV',
    'StreamingMovies'
]

for column in service_columns:
    churn_rate = df.groupby(column)['Churn'].apply(
        lambda x: (x == 'Yes').mean() * 100
    )

    print(f'\nChurn Rate by {column}:')
    print(churn_rate.round(2))
```

#### Q10. Which customer characteristics are most strongly associated with churn?

Used correlation analysis to examine the relationship between churn and selected numerical variables.

The churn variable was converted into a binary representation before calculating correlations.

```python
corr_df = df[
    ['tenure', 'MonthlyCharges', 'TotalCharges']
].copy()

corr_df['Churn'] = df['Churn'].map({
    'No': 0,
    'Yes': 1
})

corr_matrix = corr_df.corr()

print(
    corr_matrix['Churn'].sort_values(ascending=False)
)

plt.figure(figsize=(6, 4))

sns.heatmap(
    corr_matrix,
    annot=True,
    cmap='coolwarm',
    fmt='.2f',
    center=0
)

plt.title('Correlation Between Numerical Features and Churn')
plt.tight_layout()
plt.show()
```

#### Q11. What strategies could management implement to reduce customer churn?

Based on the findings from the preceding business questions, the following management strategies were proposed:

| Key Finding | Proposed Management Strategy |
|---|---|
| A considerable proportion of customers discontinue their subscriptions. | Develop customer retention programmes focused on identifying and engaging customers who are likely to leave. |
| Senior citizens, customers without partners and customers without dependents experience higher churn. | Investigate the needs of these customer segments and develop targeted retention campaigns. |
| New customers experience considerably higher churn than medium-term and long-term customers. | Introduce structured onboarding programmes, early customer engagement and incentives for new customers. |
| Month-to-month contract subscribers experience substantially higher churn. | Encourage longer-term contracts through attractive discounts, loyalty benefits and flexible subscription options. |
| Electronic check users experience considerably higher churn. | Investigate potential payment difficulties and encourage convenient and reliable payment methods. |
| Churned customers have higher average monthly spending than retained customers. | Review pricing structures and introduce affordable service packages that provide sufficient customer value. |
| Customers without additional services generally experience higher churn. | Promote complementary services through affordable bundles and targeted subscription offers. |
| Customers with longer tenure tend to have lower churn. | Strengthen customer loyalty programmes and long-term customer engagement. |
| Customers without dependents generate the largest aggregate monthly revenue among the demographic groups analysed. | Monitor revenue contributions across customer segments and develop appropriate retention initiatives. |

These strategies are recommendations based on observed patterns in the dataset. Their effectiveness would need to be tested and monitored before drawing conclusions about their impact.

## Findings

The analysis produced the following key findings:

### 1. Customer Churn
- Total customers: **7,043**
- Churned customers: **1,869**
- Retained customers: **5,174**
- Overall churn rate: **26.54%**
- Retention rate: **73.46%**

### 2. Monthly Revenue
The total monthly revenue represented by customer monthly charges was **$456,116.60**.

### 3. Customer Demographics
- Senior citizens recorded a churn rate of **41.68%**, compared with **23.61%** among non-senior customers.
- Customers without partners recorded a churn rate of **32.96%**, compared with **19.66%** among customers with partners.
- Customers without dependents recorded a churn rate of **31.28%**, compared with **15.45%** among customers with dependents.
- Gender differences in churn were relatively small.

### 4. Customer Tenure
Churn was substantially higher among newer customers.

| Customer Group | Churn Rate |
|---|---:|
| New customers (0–12 months) | 47.44% |
| Medium-term customers (13–48 months) | 23.64% |
| Long-term customers (49–72 months) | 9.51% |

### 5. Contract Type
Month-to-month customers recorded the highest churn rate.

| Contract Type | Churn Rate |
|---|---:|
| Month-to-month | 42.71% |
| One year | 11.27% |
| Two year | 2.83% |

### 6. Payment Method
Electronic check users recorded a considerably higher churn rate than customers using other payment methods.

| Payment Method | Churn Rate |
|---|---:|
| Electronic check | 45.29% |
| Mailed check | 19.11% |
| Bank transfer (automatic) | 16.71% |
| Credit card (automatic) | 15.24% |

### 7. Revenue by Customer Segment
- Customers without dependents generated the largest aggregate monthly revenue among the demographic groups analysed: **$330,524.85**.
- Customers with partners generated **$230,574.85**, compared with **$225,541.75** among customers without partners.
- Revenue contributions between male and female customers were relatively similar.

### 8. Average Monthly Spending
Churned customers had higher average monthly charges than retained customers.

| Customer Status | Average Monthly Charges |
|---|---:|
| Churned | $74.44 |
| Retained | $61.27 |

### 9. Additional Services
Customers without services such as online security and tech support generally recorded higher churn rates than customers subscribed to these services.

For example:
- Customers without online security: **41.77%** churn.
- Customers with online security: **14.61%** churn.
- Customers without tech support: **41.64%** churn.
- Customers with tech support: **15.17%** churn.

### 10. Correlation Analysis
The correlation analysis identified the following relationships with churn:

| Variable | Correlation with Churn |
|---|---:|
| MonthlyCharges | 0.193 |
| TotalCharges | -0.198 |
| Tenure | -0.352 |

Tenure had the strongest negative correlation with churn among the numerical variables examined. Monthly charges had a positive correlation, while total charges had a negative correlation.

## Reports

The project includes the following analytical deliverables:

| Deliverable | Description |
|---|---|
| Python Jupyter Notebook | Data cleaning, exploratory data analysis, visualisations and business question investigations. |
| Power BI Dashboard | Interactive presentation of customer churn, retention and revenue metrics. |
| Dashboard Preview | Image showing the Power BI dashboard. |
| Original Dataset | IBM Telco Customer Churn customer-level dataset. |

## Conclusion

The analysis indicates that customer churn is associated with several customer characteristics and account-related factors. New customers, month-to-month contract subscribers, electronic check users and customers without additional services represent important areas for further investigation.

The findings also show that churned customers have higher average monthly charges than retained customers, highlighting the importance of understanding customer value perceptions and pricing.

From a management perspective, the priority should be to strengthen early customer engagement, review pricing and service packages, encourage longer-term contracts, improve payment convenience and introduce targeted retention initiatives.

Ultimately, the business should use these insights to develop measurable retention strategies, monitor their performance and evaluate whether they reduce customer churn while protecting recurring revenue.
