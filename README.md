# SQL + Data Cleaning: Retail Sales Database Audit

> Audited a retail company's unreliable sales database, identified 213 data 
> quality issues across 11 categories, built a 6-step SQL cleaning pipeline, 
> and validated results with 7 automated checks before delivering executive insights.

---

## Business Problem

A mid-size U.S. retail company needed a regional profitability report — but the 
data team flagged the sales database as unreliable. Before any analysis could be 
trusted, a full audit and cleaning pipeline was required.

**My role:** Audit → Clean → Validate → Analyze

---

## What I Found (Audit Results)

| Issue | Table | Count | Severity |
|-------|-------|-------|----------|
| Null ship_date | orders | 81 | Medium |
| Inconsistent segment casing | customers | 26 | Medium |
| Inconsistent category casing | orders | 20 | Medium |
| Null emails | customers | 18 | Medium |
| Orphaned customer_id (FK violation) | orders | 15 | **Critical** |
| Duplicate order rows | orders | 12 | High |
| Ship date before order date | orders | 10 | High |
| Duplicate customer records | customers | 10 | High |
| Zero sales | orders | 8 | High |
| Null city | customers | 8 | Low |
| Impossible discount > 1.0 | orders | 5 | High |

**Total: 213 issues across 11 categories**  
**$28,554 in orphaned revenue identified — unattributable to any customer**

---

## Cleaning Pipeline (6 Steps)
```sql
-- Step 1: Deduplicate customers      → 310 rows (0 removed)
-- Step 2: Standardize casing + nulls → Segments, emails, cities, dates
-- Step 3: Deduplicate orders         → 2012 → 2000 rows (12 removed)
-- Step 4: Standardize category casing
-- Step 5: Remove invalid rows        → 2000 → 1970 rows (30 removed)
-- Step 6: Remove orphaned FK records → 1970 → 1956 rows (14 removed)
```

**Raw: 2,012 orders → Clean: 1,956 orders**

---

## Validation (7/7 Checks Passed)
```
✅ PASS  |  No duplicate customer_ids
✅ PASS  |  No duplicate order_ids
✅ PASS  |  No discount > 1.0
✅ PASS  |  No zero/negative sales
✅ PASS  |  No orphaned customer_ids
✅ PASS  |  All segments valid
✅ PASS  |  All categories valid
```

---

## Key Business Findings

| Finding | Detail |
|---------|--------|
| **Total Revenue** | $4,342,139 across 1,956 clean orders |
| **Top Region** | East — $1.54M revenue, 19.6% margin (highest) |
| **Top Category** | Technology — $2.81M (64% of total revenue) |
| **Best Value Segment** | Home Office — $16K revenue per customer |
| **Overall Margin** | 18.5% |

---

## Visualizations

| Chart | Insight |
|-------|---------|
| ![Audit](visualizations/05_data_quality_audit.png) | 213 issues by severity |
| ![Region](visualizations/02_regional_performance.png) | East leads revenue + margin |
| ![Category](visualizations/03_category_performance.png) | Technology dominates |
| ![Trend](visualizations/01_monthly_trend.png) | 3-year revenue trend |
| ![Segment](visualizations/04_segment_analysis.png) | Home Office highest value |

---

## Tools & Skills Demonstrated

- **SQL:** SELECT, JOIN, GROUP BY, HAVING, CASE WHEN, COALESCE, CAST, SUBSTR, NULLIF
- **Python:** pandas, matplotlib, sqlite3
- **Concepts:** Data auditing, ETL pipeline, referential integrity, FK validation, date standardization

---

## Project Structure
```
sql-data-cleaning/
├── data/
│   ├── customers.csv        ← Raw customer data (310 rows)
│   └── orders.csv           ← Raw order data (2,012 rows)
├── notebooks/
│   └── sql_data_cleaning.ipynb
├── outputs/
│   ├── customers_clean.csv  ← Validated (310 rows)
│   └── orders_clean.csv     ← Validated (1,956 rows)
├── visualizations/
│   ├── 01_monthly_trend.png
│   ├── 02_regional_performance.png
│   ├── 03_category_performance.png
│   ├── 04_segment_analysis.png
│   └── 05_data_quality_audit.png
└── portfolio/
    └── SQL_DataCleaning_CaseStudy_Vada.pdf
```

---

## Part of My Data Analytics Portfolio

| Project | Tools | Impact |
|---------|-------|--------|
| [E-Commerce Dashboard](https://github.com/vadayogi/ecommerce-dashboard) | GA4, Looker Studio | $267K opportunity |
| [Customer Segmentation](https://github.com/vadayogi/customer-segmentation) | Python, K-Means | $1.2M opportunity |
| [Churn Prediction](https://github.com/vadayogi/customer-churn-prediction) | Python, scikit-learn | $231K saved |
| **SQL + Data Cleaning** | SQL, Python | 213 issues resolved |
