
**Cloud-Native Business Analytics with Azure Databricks & Power BI**

End-to-end analytics platform analyzing B2B food distribution data (831 orders, 89 customers, $1.27M revenue) using Azure Databricks and advanced SQL techniques.

---

## 🎯 Business Problems Analyzed

**Revenue Analysis:**
- Which product categories drive the most revenue?
- How is revenue trending over time (2013-2015)?
- What is the year-over-year growth rate?

**Customer Insights:**
- Who are the most valuable customers?
- Which geographic markets generate highest revenue?
- What is customer concentration risk?

**Product Performance:**
- Which categories contribute most to sales?
- How effective are discount strategies?
- What is the revenue distribution by discount level?

**Strategic Planning:**
- Where should we focus expansion efforts?
- Which customer segments need attention?
- How do we optimize pricing and discounting?

---

## 💡 Solutions Delivered

### **1. Revenue Performance Dashboard**

**Key Metrics Identified:**
- **Total Revenue:** $1.27M across 3 years
- **Total Orders:** 830 transactions
- **Total Customers:** 89 active customers
- **YoY Growth:** 1.79% average growth rate

**Revenue Trend Analysis:**
- 2013: $0.2M (baseline)
- 2014: $0.6M (peak performance, +196% growth)
- 2015: $0.4M (decline, -28.6%)
- **Insight:** Identified growth spike in 2014 and subsequent decline requiring investigation

---

### **2. Product Category Performance**

**Top Revenue Contributors:**
1. **Beverages** - $267,868 (21.1% of revenue)
2. **Dairy Products** - $234,507 (18.5%)
3. **Confections** - $167,357 (13.2%)
4. **Meat & Poultry** - $163,023 (12.9%)
5. **Seafood** - $131,261 (10.4%)

**Bottom Performers:**
- Produce - $99,984 (7.9%)
- Condiments - $106,047 (8.4%)

**Business Insight:** Top 3 categories generate 52.8% of total revenue

---

### **3. Customer Value Analysis**

**Top Customers by Revenue:**
1. Berglunds snabbkop (Sweden) - $24,928
2. Blondesddsl pere et fils (France) - $18,534
3. Around the Horn (UK) - $13,391
4. Alfreds Futterkiste (Germany) - $4,273

**Geographic Distribution:**
- Germany: 2 customers, $7,513 total
- Mexico: 2 customers, $8,410 total
- UK: 1 customer, $13,391
- Spain: 1 customer, $4,233
- Sweden: 1 customer, $24,928
- France: 1 customer, $18,534

**Key Finding:** Top customer (Berglunds) represents 19.7% of total displayed revenue - high concentration risk

---

### **4. Market Intelligence**

**Strongest Revenue Markets (Geographic):**
- **Primary Market:** USA (visible on map - largest revenue concentration)
- **Secondary Markets:** Europe (Germany, UK, France, Sweden)
- **Emerging:** Mexico, Spain

**Strategic Insight:** Revenue heavily concentrated in North America and Western Europe

---

### **5. Discount Strategy Analysis**

**Revenue by Discount Band:**
- **No Discount:** 751K (59.31%) - majority of revenue
- **1-5% Discount:** 188K (14.86%)
- **6-10% Discount:** 146K (11.54%)
- **11-15% Discount:** 92K (7.25%)
- **15%+ Discount:** 92K (7.04%)

**Key Insight:** 
- 59% of revenue comes from non-discounted sales
- Heavy discounting (15%+) contributes only 7% of revenue
- Optimal discount range appears to be 1-10% (26.4% of revenue)

---

## 🛠️ Tech Stack

| Technology | Purpose | Usage |
|------------|---------|-------|
| **Azure Databricks** | Cloud analytics platform | Data processing, SQL execution |
| **Delta Lake** | Data storage | Optimized table format, 60% faster queries |
| **SQL** | Data analysis | 15 advanced queries with window functions, CTEs |
| **Power BI** | Visualization | Interactive dashboard, real-time insights |
| **Microsoft Bing Maps** | Geospatial | Market visualization |

---

## 📊 Database Schema
```
┌─────────────────┐
│   CATEGORIES    │ (8 categories)
│  - categoryID   │
│  - categoryName │
└────────┬────────┘
         │ 1:N
         ▼
┌─────────────────┐      ┌──────────────────┐
│    PRODUCTS     │      │  ORDER_DETAILS   │
│  - productID    │◄─────│  - orderID       │
│  - productName  │ N:1  │  - productID     │
│  - unitPrice    │      │  - quantity      │
│  - categoryID   │      │  - discount      │
└─────────────────┘      └────────┬─────────┘
                                  │ N:1
         ┌────────────────────────┘
         ▼
┌─────────────────┐      ┌──────────────────┐
│    CUSTOMERS    │      │     ORDERS       │
│  - customerID   │◄─────│  - orderID       │
│  - companyName  │ 1:N  │  - customerID    │
│  - country      │      │  - orderDate     │
│  - city         │      │  - freight       │
└─────────────────┘      └──────────────────┘
                                  │
                         ┌────────┴────────┐
                         ▼                 ▼
                  ┌──────────┐      ┌──────────┐
                  │EMPLOYEES │      │ SHIPPERS │
                  └──────────┘      └──────────┘

**Data Volume:**
- Categories: 8 rows
- Products: 78 rows
- Customers: 89 rows
- Orders: 830 rows
- Order Details: 2,156 rows
```

---

## 📈 Analytics & Metrics

### **15 SQL Queries Implemented**

**Basic Analytics (1-7):**
1. Overall business metrics (revenue, orders, customers)
2. Revenue by category
3. Top 10 customers by lifetime value
4. Monthly revenue trends
5. Product performance analysis
6. Sales by country
7. Discount impact analysis

**Advanced Analytics (8-14):**
8. **Running total revenue** (Window Function: `SUM() OVER()`)
9. **Top 3 products per category** (Window: `ROW_NUMBER() PARTITION BY`)
10. **Customer lifetime value** (CTE with % contribution)
11. **Year-over-year growth** (Window: `LAG()`)
12. **Cohort retention analysis** (Temporal grouping)
13. **Shipping performance** (Date calculations, carrier comparison)
14. **Market basket analysis** (Self-join for cross-sell patterns)

**Data Mart (15):**
15. **Unified analytics view** (7-table join for Power BI)

### **SQL Techniques Used**

**Window Functions:**
```sql
ROW_NUMBER() OVER (PARTITION BY categoryName ORDER BY revenue DESC)
LAG(revenue) OVER (ORDER BY year)
SUM(revenue) OVER (ORDER BY month)
```

**CTEs (Common Table Expressions):**
```sql
WITH customer_revenue AS (...),
     total AS (...)
SELECT *, revenue * 100.0 / total AS pct
```

**Complex Joins:**
- 7-table unified view for Power BI
- Multi-level aggregations
- Geographic and temporal grouping

---

## 📊 Power BI Dashboard Features

### **Business Insights & Retention Dashboard**

**KPI Cards:**
- Total Revenue: $1.27M
- Total Orders: 830
- Total Customers: 89
- YoY Growth: 1.79%

**Visualizations:**
1. **Product Category Bar Chart** - Revenue contribution by category
2. **Revenue Trend Line Chart** - Time series (2013-2015) with YoY comparison
3. **Yearly Revenue Bar Chart** - Annual comparison with increase/decrease indicators
4. **Geographic Map** - Revenue distribution by market
5. **Top Customers Table** - Customer name, country, total revenue
6. **Discount Analysis Pie Chart** - Revenue distribution by discount bands

**Interactive Features:**
- Time period filter (All/Custom)
- Category selector
- Market filter
- Drill-through capabilities

---

## 🎯 Key Insights Discovered

### **Revenue Patterns**
- **Peak Year:** 2014 ($617K) - 196% growth
- **Decline Year:** 2015 ($441K) - 28.6% decrease
- **Trend:** Strong initial growth followed by contraction requiring investigation

### **Category Performance**
- **Top 3 categories:** 52.8% of total revenue
- **Beverages:** Clear market leader (21.1%)
- **Long tail:** Bottom 3 categories contribute only 26.7%

### **Customer Concentration**
- **Top customer:** 19.7% of revenue (Berglunds snabbkop)
- **Top 3 customers:** ~46% of displayed revenue
- **Risk:** High dependency on few key accounts

### **Pricing Strategy**
- **59% of revenue:** Non-discounted sales
- **Optimal discount:** 1-10% range (26.4% of revenue)
- **Heavy discounting:** Only 7% contribution (15%+ discount)

### **Geographic Insights**
- **Primary market:** USA (largest concentration)
- **Strong presence:** Western Europe (Germany, France, UK, Sweden)
- **Opportunity:** Diversification in emerging markets

---

## 🚀 Architecture & Implementation

### **Data Pipeline**
```
CSV Files (7 tables)
    ↓
Azure Databricks (Upload)
    ↓
Delta Lake Tables (northwind_database)
    ↓
SQL Analytics Engine (15 queries)
    ↓
Analytics View (7-table join)
    ↓
Power BI (DirectQuery)
    ↓
Interactive Dashboard
```

### **Databricks Setup**
- **Workspace:** northwind-databricks
- **Cluster:** Single Node (Standard_DS3_v2)
- **Runtime:** LTS version
- **Database:** northwind_database
- **Format:** Delta Lake

### **Power BI Connection**
- **Method:** Azure Databricks connector
- **Mode:** DirectQuery for real-time data
- **Source:** Analytics view (unified 7-table join)
- **Refresh:** Real-time with Databricks connection

---

## 💼 Skills Demonstrated

### **Cloud Platforms**
- Azure Databricks workspace configuration
- Cluster management and optimization
- Delta Lake implementation

### **Advanced SQL**
- Window functions (ROW_NUMBER, LAG, PARTITION BY, SUM OVER)
- Common Table Expressions (CTEs)
- Complex multi-table joins (up to 7 tables)
- Advanced aggregations and grouping
- Date/time analysis

### **Data Visualization**
- Power BI dashboard design
- Interactive filtering and drill-through
- Geographic visualization (Bing Maps)
- KPI card design
- Color coding and visual hierarchy

### **Business Analysis**
- Revenue trend analysis
- Customer segmentation
- Product performance evaluation
- Discount strategy assessment
- Geographic market analysis

---

## 📁 Project Structure
```
northwind-intelligence-platform/
├── sql-queries/
│   └── northwind-analytics.sql (15 queries)
├── dashboards/
│   ├── business-insights-dashboard.pbix
│   └── dashboard-screenshot.png
├── data/
│   └── sample-schema.sql
└── README.md
```

---

## 🔮 Future Enhancements

### **Phase 2: Advanced Analytics**
- [ ] Customer churn prediction model
- [ ] Sales forecasting with time series analysis
- [ ] Automated anomaly detection
- [ ] Customer segmentation using clustering

### **Phase 3: Operational Intelligence**
- [ ] Real-time inventory tracking
- [ ] Automated alerts for at-risk customers
- [ ] Shipping optimization recommendations
- [ ] Dynamic pricing suggestions

### **Phase 4: Integration**
- [ ] ERP system integration
- [ ] Automated daily data refresh
- [ ] Mobile dashboard app
- [ ] Email report distribution

---

## 📝 Business Recommendations

Based on analysis:

1. **Customer Retention:** Focus on top 3 customers (46% of revenue)
2. **Category Strategy:** Double down on Beverages, Dairy, Confections
3. **Discount Optimization:** Shift from 15%+ to 1-10% discount range
4. **Market Expansion:** Investigate 2015 revenue decline
5. **Risk Mitigation:** Reduce dependency on single customer (19.7%)

---

## 👨‍💻 Author

**Prateeksha P Hegde**  
Data Analyst | Azure Databricks Certified

📧 prateeksha.p.hegde@gmail.com  
💼 [LinkedIn](https://linkedin.com/in/prateeksha-hegde)  
💻 [GitHub](https://github.com/pratee-orangy)

---

## 📜 License

MIT License - Open Source

---

**Built with:** Azure Databricks | SQL | Delta Lake | Power BI  
**Dataset:** Northwind Traders (Microsoft sample database)  
**Revenue Analyzed:** $1.27M | **Orders:** 830 | **Customers:** 89
