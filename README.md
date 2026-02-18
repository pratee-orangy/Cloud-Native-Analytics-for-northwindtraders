Project title : Cloud-Native Analytics for Customer Retention and Price Optimization

**Cloud-Native Analytics Platform | Azure Databricks + SQL + Power BI**

Advanced SQL analytics project demonstrating cloud data engineering and business intelligence using Azure Databricks, processing 831 orders from 92 customers across 8 product categories.

---

## Tech Stack

- **Azure Databricks** - Cloud analytics platform
- **Delta Lake** - Optimized data storage
- **SQL** - Advanced analytics (Window Functions, CTEs, Complex Joins)
- **Power BI** - Interactive dashboards

---

## Project Overview

**Dataset:** Northwind Traders (B2B food import/export)  
**Scale:** 7 tables, 2,200+ records  
**Revenue Analyzed:** $1,265,793.04  
**Time Period:** 2013-2015

---

## Database Schema
```
categories (8 rows)
    ↓
products (78 rows)
    ↓
order_details (2,156 rows)
    ↓
orders (831 rows)
    ↓
customers (92 rows)
```

---

## SQL Analytics (15 Queries)

### Basic Analytics (1-7)
1. Overall business metrics
2. Revenue by category
3. Top 10 customers
4. Monthly sales trends
5. Product performance
6. Sales by country
7. Discount impact analysis

### Advanced Analytics (8-14)
8. **Running total revenue** (Window Function: SUM OVER)
9. **Top 3 products per category** (Window Function: ROW_NUMBER with PARTITION BY)
10. **Customer lifetime value** (CTE with percentage contribution)
11. **Year-over-year growth** (Window Function: LAG)
12. **Cohort retention analysis** (Temporal grouping)
13. **Shipping performance** (Date calculations)
14. **Market basket analysis** (Self-join)

### Data Mart (15)
15. **Unified analytics view** (7-table join, 30+ metrics)

---

## SQL Techniques Demonstrated

**Window Functions:**
- `ROW_NUMBER()` - Ranking within groups
- `LAG()` - Previous period comparisons
- `SUM() OVER()` - Running totals
- `PARTITION BY` - Group-level calculations

**CTEs (Common Table Expressions):**
- Multi-level data aggregation
- Percentage calculations
- Reusable query components

**Complex Joins:**
- 4-5 table joins
- Left/inner joins
- Self-joins for market basket

**Advanced SQL:**
- CASE statements for segmentation
- Date/time functions
- Aggregate functions with GROUP BY
- HAVING clauses

---

## Key Insights

**Revenue Metrics:**
- Total Revenue: $1,265,793
- Average Order Value: $1,523
- Total Orders: 831
- Active Customers: 92

**Top Categories:**
1. Beverages - $267,868 (21.2%)
2. Dairy Products - $234,507 (18.5%)
3. Confections - $167,357 (13.2%)

**Customer Insights:**
- Top 20% customers → 45% of revenue
- Average customer lifetime value: $13,802
- 65% retention rate at 3 months

**Growth:**
- 2013→2014: +196.5% YoY growth
- 2014→2015: -28.6% decline

---

## Power BI Dashboards

**3 Interactive Dashboards:**
1. **Sales Overview** - Revenue trends, top products, geographic distribution
2. **Customer Analytics** - Lifetime value, retention, segmentation
3. **Product Performance** - Category analysis, top performers, discount impact

**Key Features:**
- Direct Databricks connection
- Real-time data refresh
- Drill-through capabilities
- Dynamic filtering

---

## Technical Implementation

### 1. Azure Databricks Setup
```
- Created workspace: northwind-databricks
- Cluster: Single Node (Standard_DS3_v2)
- Database: northwind_database
- Storage: Delta Lake format
```

### 2. Data Ingestion
```
Uploaded 7 CSV files → Delta Lake tables:
✓ categories
✓ customers  
✓ employees
✓ order_details
✓ orders
✓ products
✓ shippers
```

### 3. SQL Analytics
```
- 15 advanced SQL queries
- Created analytics view for Power BI
- Optimized with Delta Lake
```

### 4. Power BI Integration
```
- Connected via Databricks SQL endpoint
- Imported analytics view
- Built 3 dashboards
```

---

## Skills Demonstrated

**Cloud Platforms:**
- Azure Databricks workspace management
- Cluster configuration and optimization
- Delta Lake implementation

**Advanced SQL:**
- Window functions (ROW_NUMBER, LAG, PARTITION BY)
- Common Table Expressions (CTEs)
- Complex multi-table joins
- Query optimization

**Data Analytics:**
- Customer lifetime value analysis
- Cohort retention tracking
- Revenue trend analysis
- Market basket analysis

**Business Intelligence:**
- Power BI dashboard development
- KPI design and calculation
- Data modeling
- Interactive visualizations

---

## How to Run

### Prerequisites
- Azure account with Databricks access
- Power BI Desktop
- Northwind CSV files

### Setup
1. Create Azure Databricks workspace
2. Create cluster
3. Upload CSV files to create tables
4. Run SQL queries in SQL Editor
5. Connect Power BI to Databricks
6. Import analytics view
7. Build dashboards

---

## Sample SQL

**Window Function Example:**
```sql
-- Top 3 products per category
WITH product_revenue AS (
    SELECT 
        categoryName,
        productName,
        SUM(revenue) AS revenue,
        ROW_NUMBER() OVER (
            PARTITION BY categoryName 
            ORDER BY SUM(revenue) DESC
        ) AS rank
    FROM analytics
    GROUP BY categoryName, productName
)
SELECT * FROM product_revenue WHERE rank <= 3;
```

**CTE Example:**
```sql
-- Customer lifetime value with percentage
WITH customer_revenue AS (
    SELECT customerID, SUM(revenue) AS ltv
    FROM orders GROUP BY customerID
),
total AS (
    SELECT SUM(ltv) AS total FROM customer_revenue
)
SELECT 
    customerID, 
    ltv,
    ROUND(ltv * 100.0 / (SELECT total FROM total), 2) AS pct
FROM customer_revenue
ORDER BY ltv DESC;
```

---

## Project Structure
```
northwind-intelligence-platform/
├── sql-queries/
│   └── northwind-analytics.sql (All 15 queries)
├── powerbi/
│   └── Northwind_Dashboard.pbix
├── screenshots/
│   ├── query-8-running-total.png
│   ├── query-9-top-3-per-category.png
│   ├── query-10-customer-ltv.png
│   └── dashboard-overview.png
└── README.md
```

---

## Results

**Business Metrics Delivered:**
- Identified top customer segment ($110K+ lifetime value)
- Tracked 196% revenue growth (2013-2014)
- Analyzed product performance across 8 categories
- Calculated cohort retention over 24 months
- Discovered product affinity patterns for cross-selling

**Technical Achievements:**
- 15 production-ready SQL queries
- Cloud-based analytics infrastructure
- Real-time Power BI dashboards
- Delta Lake optimization

---

## Author

**Prateeksha P Hegde**  
Data Analyst | Azure Databricks Certified

📧 prateeksha.p.hegde@gmail.com  
💼 [LinkedIn](https://linkedin.com/in/prateeksha-hegde)  
💻 [GitHub](https://github.com/pratee-orangy)

---

**Built with Azure Databricks, SQL, and Power BI**

