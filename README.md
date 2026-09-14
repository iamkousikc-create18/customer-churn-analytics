# Customer Churn Analysis & Data Pipeline

An end-to-end data engineering and analytics pipeline that extracts customer telemetry from an SQLite database, handles missing values/structural discrepancies, performs feature engineering, and provides actionable churn insights using Pandas, Seaborn, and Matplotlib.

## 📊 Business Metrics Summary
* **Overall Churn Rate:** 28.57%
* **Overall Retention Rate:** 71.43%
* **Average Revenue Per User (ARPU):** ₹18.85 / \$18.85 per month
* **Escalation Rate:** 19.05% of support tickets get escalated
* **Churn-Escalation Correlation:** 0.77 (Strong positive link between support issues and account cancellations)

---

## 🛠️ Data Pipeline Architecture

### 1. Ingestion & Dynamic Multi-Table Schema Extraction
The pipeline establishes a live connection to `customer_churn.db`, queries `sqlite_master` to retrieve all tables dynamically, reads individual relational tables, and spins them up into global memory frames.
* **`df_db_customer`**: Core metadata containing customer bios and demographics.
* **`df_db_subscription`**: Financial metrics, billing terms, account lifecycle flags.
* **`df_db_support`**: Incident histories, CSAT surveys, ticket routing info.

### 2. Advanced Preprocessing & Data Quality Enhancements
* **Missing Value Imputation via Spatial Mapping**: Discovered `None` data records across the `country` column. Developed a cross-reference dictionary mapping states to countries (`state_country_mapping`) to systematically impute missing fields based on verified geographic locations.
* **Categorical String Harmonization**: Cleaned categorical label variations in the `gender` feature by standardizing redundant entries (`"Men"` ➡️ `"Male"`, `"Women"` ➡️ `"Female"`).
* **Dimensionality Selection**: Dropped completely unpopulated structural blocks (`pincode`) and low-variance features (`interests`).
* **Temporal Parsing**: Coerced timestamp records from raw text formats into native datetime64 metrics across structural attributes (`dob`, `subscription_start_date`, `renewal_date`, `cancellation_date`, `complaint_date`).

### 3. Feature Engineering & Multi-Source Synthesis
* **Incident Frequency Weighting**: Engineered a `complaint_count` feature using window-based group transforms (`transform("count")`) to accurately record cumulative user stress levels.
* **Deduplication Strategy**: Sorted complaints chronologically and dropped duplicate records using `keep="last"` to retain only the most critical, final interaction per user.
* **Multi-Key Table Union**: Evaluated unique customer counts across data subsets to perform an optimized multi-stage left-join sequence on the parent primary key (`customerid`).
* **Lifecycle Tenure Engineering**: Formulated a time delta calculation logic to establish continuous user lifetimes:
  \[\text{Tenure} = \begin{cases} \text{cancellation\_date} - \text{subscription\_start\_date} & \text{if Churned} \\ \text{current\_date} - \text{subscription\_start\_date} & \text{if Active} \end{cases}\]

---

## 📉 Core Visualizations & Exploratory Data Analysis

### Churn Risk Prioritization Matrix
Implemented prioritizing rules to bin operational risk boundaries:
* **Low Risk**: Churn score < 50
* **Mid Risk**: Churn score ≥ 50 and < 70
* **High Risk**: Churn score ≥ 70

```python
# Priority Encoding Matrix for Feature Correlations
order_mappings = {
    "plan_type": ["Basic", "Standard", "Premium"],
    "contract_type": ["Monthly", "Annual"],
    "churn_risk": ["Low", "Mid", "High"]
}
```

### Key Performance Charts In The Dataset
1. **Monthly Churn Trend Line**: Visualizes timeline spikes in user structural cancellations.
2. **Churn Density by Tier**: Highlights that **Basic Plan** users experience the highest churn rate (60.00%), compared to **Premium Plan** users (14.29%).
3. **Regional Hotspot Risk**: Pinpoints geographic distributions showing critical high-churn territories (e.g., Karnataka at 100.00% churn rate).

---

## 🚀 Getting Started

### Prerequisites
Make sure you have the following packages installed:
```bash
pip install numpy pandas matplotlib seaborn
```

### Execution Layout
Run the Jupyter notebook cells sequentially. The cleaned, aggregated dataset will be written to disk in a flat-file exchange system format:
```python
df.to_csv("exported_churn_data.csv", index=False)
