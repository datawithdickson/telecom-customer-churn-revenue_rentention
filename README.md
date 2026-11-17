# Telecom Customer Churn & Revenue Retention Analysis

## Project Overview

This project analyses customer churn and recurring revenue patterns in a telecommunications customer dataset. The work combines Python-based exploratory data analysis with a Power BI dashboard to examine customer groups and account characteristics associated with churn.

## Business Objectives

- Measure overall customer churn and retention.
- Examine churn across customer demographics, tenure, contract types, payment methods and service subscriptions.
- Compare monthly revenue and spending patterns for churned and retained customers.
- Translate observed patterns into practical customer-retention considerations.

## Business Questions Addressed

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

## Tools & Technologies

- **Python** — data preparation, exploratory analysis and visualisation.
- **Jupyter Notebook** — analytical workflow and documentation.
- **Power BI** — interactive dashboard and business reporting.
- **CSV** — source dataset.

## Repository Structure

```text
Telecom_Customer_Churn_Revenue_Retention/
├── README.md
├── Data/
│   └── telco_customer_churn.csv
├── Python/
│   └── telecom_churn_analysis.ipynb
├── Dashboard/
│   ├── telecom_churn_retention_dashboard.pbix
│   └── dashboard_preview.png
└── Project-Image/
    └── [Add project cover image here]
```

## Methodology

1. Load the source customer dataset and inspect its structure.
2. Explore customer demographics, account information, services, billing and churn.
3. Clean relevant fields and prepare the data for analysis.
4. Conduct univariate and bivariate analysis to investigate the business questions.
5. Present selected customer and revenue metrics in an interactive Power BI dashboard.

## Key Areas of Analysis

- Customer demographics and household characteristics.
- Customer tenure and contract type.
- Internet and additional service subscriptions.
- Payment methods and billing.
- Churn status, monthly charges and revenue.

## Recommendations in the Analysis

The notebook discusses retention initiatives including stronger onboarding for new customers, targeted engagement for higher-churn customer segments, incentives that encourage longer-term contracts, and improvements to payment convenience and service adoption. These are proposed actions based on observed associations; their impact should be tested and monitored rather than assumed.

## Important Note

The submitted Python notebook and Power BI dashboard have not yet been reconciled to a single set of totals. The dashboard preview reports 7,032 customers, while the source dataset contains 7,043 records. Metrics should therefore be cross-checked before using them for operational decisions.

## Project Files

- The `Python/` folder contains the Jupyter Notebook analysis.
- The `Dashboard/` folder contains the Power BI report and its preview image.
- The `Data/` folder contains the source CSV dataset used in the analysis.
- The `Project-Image/` folder is reserved for a project cover image.
