# Customer Churn Analytics

An end-to-end data analytics project focused on understanding customer churn, subscription behavior, revenue impact, and customer risk for an OTT subscription platform.

## 📌 Project Overview

Customer churn is a major challenge for subscription-based businesses. This project analyzes customer, subscription, and support data to identify churn patterns, understand customer behavior, measure revenue impact, and generate actionable business insights.

The project integrates a SQLite database with Python for data extraction, cleaning, feature engineering, exploratory data analysis, KPI calculation, and visualization.

## 🎯 Business Objectives

- Measure the overall customer churn and retention rate
- Identify churn patterns across subscription plans and states
- Compare churn across different contract types
- Analyze customer tenure and subscription behavior
- Measure revenue loss and revenue at risk
- Analyze customer complaints and support escalations
- Segment customers based on churn risk
- Identify areas where customer retention strategies can be improved

## 🛠️ Tech Stack

- **Python**
- **Pandas** – Data manipulation and analysis
- **NumPy** – Numerical operations
- **SQLite** – Relational database
- **Matplotlib** – Data visualization
- **Seaborn** – Statistical visualization
- **Jupyter Notebook** – Analysis and documentation

## 🗄️ Database Structure

The project uses a SQLite database named `customer_churn.db`.

The database contains three main tables:

### 1. `db_customer`

Contains customer demographic information.

- customerid
- name
- country
- state
- gender
- dob
- interests
- pincode

### 2. `db_subscription`

Contains subscription and revenue-related information.

- customerid
- subscription_start_date
- subscription_type
- renewal_date
- plan_type
- contract_type
- cancellation_date
- cancellation_reason
- monthly_charges
- cltv
- churn_score

### 3. `db_support`

Contains customer support information.

- customerid
- complaint_date
- escalations
- csat_score
- comment

## 🔄 Project Workflow

### 1. SQL Database Integration

- Connected SQLite database with Python
- Retrieved database tables using SQL queries
- Loaded relational data into Pandas DataFrames

### 2. Data Cleaning

- Inspected dataset structure and data types
- Converted date columns into datetime format
- Checked missing and null values
- Handled missing state information
- Removed unnecessary columns
- Performed data quality checks

### 3. Data Integration

Customer, subscription, and support tables were joined using `customerid` to create a consolidated dataset for analysis.

### 4. Feature Engineering

Created analytical features such as:

- Churn flag
- Customer tenure
- Complaint count
- Churn risk category
- Churn and retention metrics

### 5. Exploratory Data Analysis

Performed analysis using:

- GroupBy
- Aggregations
- Pivot tables
- Filtering
- Correlation analysis

### 6. Data Visualization

Created visualizations to analyze:

- Monthly churn trends
- Churn by subscription plan
- Churn by state
- Correlation between important variables

## 📊 Key KPIs

The analysis calculates several business-focused KPIs:

| KPI | Description |
|---|---|
| Churn Rate | Percentage of customers who churned |
| Retention Rate | Percentage of customers retained |
| Churn by Plan | Churn rate across Basic, Standard and Premium plans |
| Churn by State | Churn distribution across locations |
| ARPU | Average revenue per active customer |
| Average Tenure | Average duration of customer subscription |
| Revenue at Risk | Revenue associated with high churn-risk customers |
| Escalation Rate | Support escalation rate |
| Average Complaints per Customer | Average number of complaints per customer |
| Escalation → Churn | Comparison of churn for customers with and without escalations |

## 📈 Key Findings

The analysis produced the following major findings:

- **Overall Churn Rate:** 28.6%
- **Retention Rate:** 71.4%
- Most churn came from the **Basic subscription plan**
- The highest churn was observed in **September 2024**
- **Karnataka** was identified as the most affected state
- **Average Customer Tenure:** approximately 1,451 days
- **ARPU:** approximately Rs 18.8
- **Total Revenue:** 395
- **Revenue Loss Due to Churn:** 74
- **CLTV Lost:** 2,047
- **Revenue Loss:** approximately 18%
- **Monthly Contract Churn:** 55.6%
- **Annual Contract Churn:** 8.3%

The analysis therefore highlights a substantial difference in churn behavior between monthly and annual contract customers. :contentReference[oaicite:2]{index=2}

## 💡 Business Insights

Based on the analysis, the following areas were identified for further investigation:

### Karnataka

Investigate whether the high churn in Karnataka is associated with:

- Pricing changes
- Customer complaints
- Technical issues
- Customer experience problems

### Basic Plan

Investigate whether pricing or subscription changes affected Basic-plan customers, particularly around September 2024.

### Competitor Activity

Monitor competitor offerings and customer switching behavior to understand whether competitive pressure is contributing to churn.

### High & Medium Risk Customers

Prioritize customers categorized as **High** and **Medium** churn risk.

Retention efforts can consider:

- Customer lifetime value
- Complaint history
- Support interactions
- Churn score

The project recommends targeted customer outreach through appropriate communication channels to address customer issues and improve retention. :contentReference[oaicite:3]{index=3}

## 📂 Repository Structure

```text
customer-churn-analytics/
│
├── Churn_Analysis.ipynb
├── customer_churn.db
├── requirements.txt
└── README.md
