#  Apple Retail Performance Analytics & Revenue Optimization

### End-to-End Retail Analytics | SQL • Python • Power BI • Business Intelligence

> Transforming 1M+ retail transactions into actionable business decisions through advanced analytics, KPI monitoring, product optimization, store benchmarking, and warranty intelligence.

---

## 📌 Executive Summary

This project simulates a real-world retail electronics business scenario where data is leveraged to optimize revenue, improve product strategy, benchmark store performance, and reduce warranty-related costs.

Using **SQL, Python, and Power BI**, I analyzed over **1 million retail transactions**, developed an executive-level analytics solution, and delivered actionable recommendations supporting business growth and operational excellence.

---

## 🎯 Business Objectives

### Revenue Analytics
- Understand revenue fluctuations over time
- Detect seasonal sales patterns
- Identify revenue anomalies

### Product Analytics
- Determine top-performing products
- Analyze category contribution
- Identify revenue concentration

### Store Analytics
- Benchmark store performance
- Identify underperforming locations
- Evaluate revenue distribution across stores

### Warranty Analytics
- Analyze warranty claim patterns
- Identify high-risk products
- Improve product quality and customer satisfaction

---

## 📊 Key Business Metrics

| KPI | Value |
|------|------|
| Total Sales | $6M |
| Total Orders | 1M |
| Warranty Claims | 30K |
| Claim Rate | 2.88% |
| Total Stores | 75 |
| Affected Products | 89 |

---

## 🏗️ Project Architecture

```text
Raw Data
   ↓
Python Data Cleaning
   ↓
SQL Data Modeling
   ↓
Exploratory Data Analysis
   ↓
Power BI Dashboard Development
   ↓
Business Insights
   ↓
Strategic Recommendations
```

---

## 🛠️ Technology Stack

| Tool | Purpose |
|--------|---------|
| MySQL | Data Extraction & Analytics |
| Python | Data Cleaning & EDA |
| Pandas | Data Manipulation |
| Matplotlib | Visualization |
| Power BI | Dashboard Development |
| DAX | KPI Calculations |
| Excel | Data Validation |

---

## 📂 Dataset Overview

```text
dataset/
│
├── sales.csv
├── products.csv
├── stores.csv
├── category.csv
└── claims.csv
```

### Dataset Scale

- 1M+ Sales Transactions
- 75 Retail Stores
- Multiple Product Categories
- 30K Warranty Claims
- Historical Data (2019–2024)

---

## 📈 Dashboard Overview
<img width="1158" height="656" alt="Screenshot 2026-06-19 203822" src="https://github.com/user-attachments/assets/1141141f-98d6-43bc-af44-aecd5e1d5d55" />

### 🏠 Executive Dashboard

#### KPIs
- Total Sales
- Total Orders
- Warranty Claims
- Claim Rate

#### Key Insights

- Revenue remained relatively stable across the analysis period.
- Product sales are concentrated among a limited set of products.
- Growth opportunities exist through cross-selling and product bundling.
- Business performance can be improved through targeted product strategies.

#### Business Recommendation

Increase Average Order Value (AOV) through bundled offerings, cross-selling initiatives, and targeted promotions.

---

### 📦 Product Performance Analysis
<img width="1170" height="655" alt="Screenshot 2026-06-19 164530" src="https://github.com/user-attachments/assets/9ac87c84-9fe3-4e75-a37b-6ff5fe3053c2" />

#### Analysis Conducted

- Revenue by Category
- Top Product Sales Trend
- Top Revenue-Generating Products
- Pareto Analysis (80/20 Rule)

#### Key Findings

- Accessories contribute the highest revenue.
- Revenue is concentrated among a small subset of products.
- Product demand exhibits seasonal behavior.
- Several products consistently outperform portfolio averages.

#### Business Recommendation

Prioritize inventory investment and marketing support for top-performing products while reducing exposure to low-performing SKUs.

---

### 🏪 Store Performance Analysis
<img width="1162" height="662" alt="Screenshot 2026-06-19 164547" src="https://github.com/user-attachments/assets/47c16dfb-cac9-4538-beed-091da1becf56" />

#### Analysis Conducted

- Top Revenue-Contributing Stores
- Bottom Performing Stores
- Revenue Benchmarking
- Monthly Revenue Trends

#### Key Findings

- Revenue distribution is uneven across stores.
- Top-performing stores significantly outperform network averages.
- Several locations consistently underperform.
- Revenue concentration suggests dependency on a small group of stores.

#### Business Recommendation

Implement location-specific marketing initiatives, optimize inventory allocation, and establish performance improvement programs for low-performing stores.

---

### 🛡️ Warranty Claims & Product Quality Analysis
<img width="1167" height="672" alt="Screenshot 2026-06-19 164604" src="https://github.com/user-attachments/assets/537ed814-e97e-4028-b7d1-24c9c66d09c4" />

#### Analysis Conducted

- Products with Highest Claims
- Warranty Claims by Category
- Monthly Claim Trends
- Repair Status Distribution

#### Key Findings

- Overall claim rate remains low at 2.88%.
- Claims are concentrated among a limited set of products.
- Accessories and Smartphone categories generate the highest claim volumes.
- Warranty activity declined during 2024.

#### Business Recommendation

Prioritize quality improvement initiatives for high-claim products and strengthen supplier performance monitoring to reduce service costs.

---

# 🧠 Advanced SQL Analytics

## 1️⃣ Monthly Revenue Trend Analysis

```sql
SELECT
    DATE_FORMAT(sale_date, '%Y-%m') AS month,
    SUM(total_amount) AS revenue
FROM sales
GROUP BY month
ORDER BY month;
```

### Business Value

- Tracks long-term revenue performance
- Detects seasonality and anomalies
- Supports forecasting

---

## 2️⃣ Store Revenue Ranking

```sql
SELECT
    store_id,
    SUM(total_amount) AS revenue,
    RANK() OVER (
        ORDER BY SUM(total_amount) DESC
    ) AS store_rank
FROM sales
GROUP BY store_id;
```

### Business Value

- Identifies top-performing stores
- Supports benchmarking
- Enables operational optimization

---

## 3️⃣ Category-wise Top Products

```sql
WITH ranked_products AS (
    SELECT
        c.category_name,
        p.product_name,
        SUM(s.quantity) AS total_sales,
        RANK() OVER (
            PARTITION BY c.category_name
            ORDER BY SUM(s.quantity) DESC
        ) AS rnk
    FROM sales s
    JOIN products p
        ON s.product_id = p.product_id
    JOIN category c
        ON p.category_id = c.category_id
    GROUP BY
        c.category_name,
        p.product_name
)

SELECT *
FROM ranked_products
WHERE rnk <= 3;
```

### Business Value

- Identifies category leaders
- Supports assortment optimization
- Improves inventory allocation

---

## 4️⃣ 7-Day Moving Average

```sql
SELECT
    sale_date,
    daily_sales,
    AVG(daily_sales) OVER (
        ORDER BY sale_date
        ROWS BETWEEN 6 PRECEDING
        AND CURRENT ROW
    ) AS moving_avg_7_days
FROM daily_sales;
```

### Business Value

- Removes short-term noise
- Highlights underlying trends
- Improves forecasting accuracy

---

## 5️⃣ Pareto Analysis (80/20 Rule)

```sql
WITH product_revenue AS (
    SELECT
        p.product_name,
        SUM(s.total_amount) AS revenue
    FROM sales s
    JOIN products p
        ON s.product_id = p.product_id
    GROUP BY p.product_name
)

SELECT *
FROM product_revenue
ORDER BY revenue DESC;
```

### Business Value

- Identifies products driving revenue
- Supports inventory prioritization
- Optimizes merchandising strategy

---

## 6️⃣ Warranty Claim Analysis

```sql
SELECT
    p.product_name,
    COUNT(c.claim_id) AS total_claims
FROM claims c
JOIN sales s
    ON c.sale_id = s.sale_id
JOIN products p
    ON s.product_id = p.product_id
GROUP BY p.product_name
ORDER BY total_claims DESC;
```

### Business Value

- Identifies quality issues
- Reduces warranty expenses
- Improves customer satisfaction

---

## 📊 Power BI Features

### Dashboard Capabilities

✔ Executive KPI Monitoring

✔ Interactive Slicers

✔ Drill-Through Analysis

✔ Dynamic Filtering

✔ DAX-Based KPI Calculations

✔ Product Analytics

✔ Store Benchmarking

✔ Warranty Intelligence

✔ Executive Reporting

---

## 💡 Strategic Business Recommendations

### Revenue Growth
- Increase product bundling opportunities
- Expand cross-selling strategies
- Launch targeted campaigns during low-demand periods

### Product Optimization
- Focus inventory on top-performing products
- Reduce low-performing inventory
- Improve product assortment planning

### Store Performance
- Replicate best practices from top-performing stores
- Develop improvement plans for underperforming stores
- Optimize regional inventory allocation

### Product Quality
- Monitor products with elevated warranty rates
- Strengthen supplier quality audits
- Improve testing and quality assurance processes

---

## 📈 Business Impact

### Revenue Optimization
Identified products responsible for the majority of revenue generation.

### Inventory Efficiency
Improved inventory allocation decisions using product-level analytics.

### Store Performance Improvement
Highlighted underperforming stores requiring targeted intervention.

### Warranty Cost Reduction
Identified products driving warranty-related service costs.

### Executive Decision Support
Delivered executive-level dashboards enabling data-driven decision-making.

---

## 🎯 Product Analytics Mindset

Unlike traditional dashboard projects, this analysis focuses on business outcomes rather than visualization alone.

### Key Questions Answered

✔ Which products generate the highest business value?

✔ Which stores contribute most to company performance?

✔ Where are operational inefficiencies occurring?

✔ Which products create the highest warranty burden?

✔ How can inventory allocation be optimized?

✔ How can revenue growth be accelerated?

---

## 🏆 Why This Project Stands Out

### ✔ Real-World Business Scenario
Built around challenges commonly faced by retail and consumer electronics organizations.

### ✔ End-to-End Analytics Workflow

```text
SQL → Python → Power BI → Business Decisions
```

### ✔ Advanced SQL
- Window Functions
- CTEs
- Ranking Functions
- Moving Averages
- Pareto Analysis

### ✔ Executive-Level Reporting
Designed for business leaders and decision-makers.

### ✔ Product Analytics Thinking
Focuses on business impact rather than dashboard creation.

### ✔ Decision-Oriented Storytelling
Every dashboard page concludes with actionable recommendations.

---

## 🚀 Recruiter Takeaway

This project demonstrates the ability to:

✔ Analyze large-scale transactional datasets

✔ Build executive-level Power BI dashboards

✔ Apply advanced SQL analytics

✔ Deliver actionable business recommendations

✔ Perform end-to-end analytics

✔ Communicate insights effectively

✔ Think like a Product Analyst, Business Analyst, and Data Analyst

---

## 👨‍💻 Author

**M Dilli Babu**

Data Analyst | SQL | Python | Power BI | Business Intelligence

🔗 Portfolio: https://dillibabuportfolio.netlify.app/

🔗 LinkedIn: https://www.linkedin.com/in/dilli-babu-2b943522b

🔗 GitHub: https://github.com/Dilli57

---

## ⭐ Support

If you found this project useful, please give it a ⭐ on GitHub.

It helps others discover the project and supports my data analytics journey.
