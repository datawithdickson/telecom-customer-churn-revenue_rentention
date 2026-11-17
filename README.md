# Telecom Customer Churn & Revenue Retention Analysis

## Project Overview
An exploratory analysis of telecommunications customer churn and recurring revenue, using Python for data analysis and Power BI for interactive reporting.

## Objectives
- Measure customer churn, retention and monthly revenue.
- Examine churn patterns across customer demographics, tenure, contracts, payment methods and subscribed services.
- Compare spending and revenue patterns between churned and retained customers.
- Translate observed patterns into practical retention considerations.

## Business Questions
1. What is the overall customer churn rate?
2. What is the company's total monthly revenue?
3. Which customer segments have the highest churn rates?
4. How does tenure influence customer churn?
5. Which contract types experience the highest churn?
6. Does payment method relate to customer churn?
7. Which customer segments generate the highest revenue?
8. How does average monthly spending differ between churned and retained customers?
9. Does having additional services relate to customer retention?
10. Which customer characteristics are most strongly associated with churn?
11. What strategies could management implement to reduce customer churn?

## Tools
- Python and pandas for data preparation and analysis
- Jupyter Notebook for the analytical workflow
- Power BI for dashboard reporting
- CSV for the source dataset

## Methodology
The workflow covers dataset loading and initial exploration, data cleaning, exploratory analysis of customer demographics, account details, services and billing, followed by analysis of the business questions. The Power BI report presents selected customer, churn and revenue metrics with interactive filters.

## Summary of Findings
The analysis highlights differences in churn across tenure, contract type, payment method, customer demographics and additional service subscriptions. Newer customers and month-to-month subscribers are notable higher-churn groups in the analysis. The notebook also observes higher average monthly charges among churned customers than retained customers. These are associations in the dataset, not proof of causation.

## Recommendations
The analysis points to strengthening early customer onboarding, investigating the needs of higher-churn segments, encouraging suitable longer-term plans, reviewing payment convenience and pricing perceptions, and improving awareness of relevant additional services. Any retention initiatives should be tested and monitored to establish their actual effect.

## Conclusion
Customer churn is not evenly distributed across the customer base. Tenure, contract arrangements, payment method and service adoption provide useful dimensions for identifying groups that may need closer attention. A targeted retention approach, supported by ongoing measurement, may help the business protect recurring revenue.

## Repository Structure
```text
.
├── README.md
├── Data/
│   └── WA_Fn-UseC_-Telco-Customer-Churn.csv
├── Python/
│   └── telecom_churn_analysis.ipynb
├── Dashboard/
│   ├── telecom_churn_retention_dashboard.pbix
│   └── dashboard_preview.png
└── Project-Image/
    └── (reserved for project cover image)
```

## Data Note
The submitted dashboard preview and notebook/source data currently show inconsistent customer totals. The notebook and dashboard are being retained as submitted; figures should be reconciled before using the report for operational decisions.
