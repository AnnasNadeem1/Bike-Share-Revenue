# 🚲 Bike Share Revenue and Pricing Analysis

## 📌 Project Overview
This project analyzes **bike share rider data** to uncover profitability trends, rider demographics, and seasonal performance.  
I used **SQL** for data processing and **Power BI** for visualization to build an interactive dashboard.  
Finally, I developed a **pricing strategy recommendation** to guide future growth.  

---

## 📊 Dashboard Preview

## Dashboard Overview
<img width="908" height="502" alt="dash" src="https://github.com/user-attachments/assets/2f57030f-8289-4562-8e33-c439fad32952" />
## Pricing Recommendation
<img width="868" height="491" alt="price" src="https://github.com/user-attachments/assets/4307e29a-6d17-4878-b9da-1af430feb22c" />
---

## 🛠️ Tech Stack
- **SQL** → data cleaning, joins, KPI calculations  
- **Power BI** → dashboard design, KPIs, visualization  
- **Excel** (optional) → preprocessing  

---

## 📂 Data Processing
1. Combined yearly datasets (`bike_share_yr_0` and `bike_share_yr_1`) using a SQL CTE.  
2. Joined with `cost_table` to calculate revenue and profit.  

```sql
with cte as (
  select * from bike_share_yr_0
  union all
  select * from bike_share_yr_1
)
select
  a.dteday,
  a.season,
  a.yr,
  a.weekday,
  a.hr,
  a.rider_type,
  a.riders,
  b.price,
  b.COGS,
  a.riders * b.price as revenue,
  (a.riders * b.price) - (a.riders * b.COGS) as profit
from cte a
left join cost_table b
  on a.yr = b.yr;
```
## 📈 KPIs, Insights & Recommendations

**Key KPIs**
- Total Riders: **3.29M**  
- Total Revenue: **$15.18M**  
- Total Profit: **$10.45M**  
- Avg. Profit Margin: **0.45**  

**Insights**
- **Peak Hours** → 10–15 (midday & evening) are most profitable.  
- **Days** → Wednesday & Friday show the strongest sales.  
- **Seasons** → Summer (Season 3) generated ~$4.9M revenue, the highest.  
- **Rider Type** → Registered riders contribute ~81% of total revenue.  

**Pricing Recommendation**
- Current avg. price: **$4.49**  
- Proposed increase: **+5% to +10%**  
  - New Price Range: $5.24 – $5.49  
- Rationale → strong growth in 2022 suggests the market can sustain a moderate increase.  

**Implementation Plan**
1. **Market Analysis** → benchmark against competitors.  
2. **Pilot & Monitor** → test for 4–8 weeks and track churn, rider behavior.  
3. **Adjust** → refine based on elasticity observed.  
4. **Communicate Value** → frame the increase as service improvements.  
