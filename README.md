# African Public Contracts: Red Flags and Outlier Analysis

A **practice project** exploring public procurement data analysis using Python, SQL, descriptive statistics, and data visualization.

> **Disclaimer:** This is an educational practice project using fictional or synthetic data. It does not use real public procurement records, represent actual government spending, or identify real cases of corruption or financial misconduct. All results and findings are illustrative and should not be interpreted as evidence about any country, ministry, or public institution.

## 📌 Project Overview

This project demonstrates a data analysis workflow designed to explore hypothetical public procurement contracts, identify statistically unusual contract values, and examine spending distributions across fictional government entities.

The analysis covers data cleaning, SQL-based aggregations, descriptive statistics, interquartile range (IQR) outlier detection, and data visualization.

The project is intended to demonstrate practical skills in data preparation, analytical reasoning, database querying, and communicating statistical findings.

## 🎯 Objectives

- Clean and transform inconsistent currency-formatted text into numeric values.
- Use SQL to aggregate contract counts and expenditure by purchasing entity.
- Apply descriptive statistics to understand the distribution of contract values.
- Calculate statistical thresholds to flag potential outliers.
- Visualize contract value distributions and outlier thresholds.
- Document analytical findings while distinguishing statistical anomalies from evidence of misconduct.

## 🛠️ Tech Stack

- **Python:** Data processing and analysis.
- **Pandas:** Data cleaning, transformation, and aggregation.
- **NumPy:** Numerical operations.
- **SQLite (`sqlite3`):** Relational database queries.
- **Matplotlib:** Data visualization.
- **Seaborn:** Statistical visualization.
- **Statistical methods:** Mean, median, standard deviation, quartiles, interquartile range (IQR), and outlier detection.

## 🔬 Analytical Workflow

### 1. Data Cleaning and Transformation

**Objective:** Convert inconsistent text-based contract values into numeric values suitable for statistical analysis.

The practice includes string manipulation, removal of currency labels and thousands separators, whitespace handling, and numeric conversion.

Example:

```python
def clean_amount(text_raw):
    text = str(text_raw)

    text = (
        text.replace("KES", "")
        .replace("UGX", "")
        .replace("reales", "")
        .replace(",", "")
        .strip()
    )

    return float(text)

df["clean_amount"] = df["tender_value"].apply(clean_amount)
```

This example illustrates a basic transformation approach. In a production workflow, currency normalization, missing values, invalid records, and conversion errors would require additional validation.

**Key skills:** Data cleaning, string manipulation, type conversion, and data quality awareness.

### 2. SQL-Based Aggregation

**Objective:** Use SQL to summarize contract counts and total contract values by purchasing entity.

The cleaned practice dataset is loaded into an in-memory SQLite database for querying.

Example:

```sql
SELECT
    buyer_name AS ministry,
    COUNT(tender_id) AS total_contracts,
    ROUND(SUM(clean_amount), 2) AS total_spent
FROM contracts
GROUP BY buyer_name
ORDER BY total_spent DESC;
```

This query demonstrates how SQL aggregation can support comparisons across entities and help identify where hypothetical expenditure is concentrated.

**Key skills:** SQL aggregation, `GROUP BY`, aggregate functions, aliases, and sorting.

### 3. Descriptive Statistics and Outlier Detection

**Objective:** Examine the distribution of contract values and calculate a statistical threshold for identifying unusually high observations.

The interquartile range method is used:

\[
IQR = Q3 - Q1
\]

\[
\text{Upper Bound} = Q3 + 1.5 \times IQR
\]

Where:

- **Q1:** 25th percentile.
- **Q3:** 75th percentile.
- **IQR:** Difference between the third and first quartiles.
- **Upper bound:** Statistical reference threshold for potential high-value outliers.

Contract values above this threshold can be flagged for further investigation. An outlier is not automatically an error, an irregularity, or evidence of corruption.

### 4. Data Visualization

The project uses Matplotlib and Seaborn to visualize the distribution of hypothetical contract values and display the upper outlier threshold.

Example visualization features include:

- Horizontal boxplots.
- Distribution summaries.
- Reference lines for statistical thresholds.
- Labels and annotations to improve interpretability.

These visualizations help communicate the analytical results and highlight observations that may warrant additional review.

## 📊 Illustrative Results

The following figures are retained from the practice analysis. They are **illustrative outputs from a non-real dataset**, not verified public procurement statistics.

| Metric | Illustrative result |
|---|---:|
| Mean contract value | $387,324.18 |
| Median contract value | $335,309.50 |
| Standard deviation | $250,586.27 |
| First quartile (Q1) | $182,562.75 |
| Third quartile (Q3) | $591,724.50 |
| Upper outlier threshold | $1,205,467.12 |
| Outliers detected | 0 |

*Currency figures are illustrative values expressed in USD for demonstration purposes.*

### Key Observations

- **Spending concentration:** The example analysis compares expenditure across hypothetical purchasing entities.
- **Distribution analysis:** Comparing the mean and median provides an initial indication of the distribution's shape.
- **Outlier detection:** The IQR method provides a reproducible statistical rule for flagging unusually high values.
- **Interpretation limits:** Detecting no outliers does not establish that all transactions are legitimate or free of risk.

These observations demonstrate the analytical process only. They do not describe actual ministries, government expenditure, or procurement risks in Kenya, Uganda, or any other country.

## ⚠️ Limitations

- The dataset is fictional or synthetic and is not a source of verified real-world evidence.
- The results depend on the assumptions and structure of the practice dataset.
- Currency labels and conversion logic in the example are simplified and are not a substitute for a validated currency-normalization process.
- The IQR method identifies statistical outliers, not corruption.
- A real procurement risk assessment would require verified source data, contextual analysis, documented indicators, and independent validation.

## 🚀 Potential Next Steps

Future extensions of this practice project could include:

- Adding validation rules for missing, negative, and malformed contract values.
- Separating currencies and applying documented exchange-rate assumptions where appropriate.
- Comparing mean, median, and percentile distributions across groups.
- Testing alternative outlier-detection methods.
- Building a dashboard to explore contract distributions and potential statistical anomalies.
- Documenting data lineage, assumptions, and reproducibility.

## 👤 Author

Developed as an independent **data analysis practice project** to strengthen skills in Python, SQL, statistics, and data visualization.

This project is for educational and portfolio demonstration purposes only. It is not an official audit, a real-world investigation, or a contribution to any organization.

---
