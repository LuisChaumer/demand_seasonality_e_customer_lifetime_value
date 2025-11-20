Mobility Analytics – Demand Seasonality & Customer Lifetime Value 🚕📊

Author: Luis Chaumer
Role: Data Analyst
Tools: Python, SQL (SQLite), Pandas, NumPy, Matplotlib

📘 Project Overview

This project analyzes demand patterns and customer lifetime value (CLV) for a fictional ride-hailing mobility service.
It uses 112,568 synthetic trips (May 2024 – May 2025) and 30,000 customers across 5 regions.

The goal is to understand:

When demand is highest (hour/day/seasonality)

What customer segments generate the most value

How to improve scheduling, marketing, and retention strategies

🎯 Project Objectives
Demand Analysis

Daily, hourly, and weekday volume patterns

Seasonality insights

Operational recommendations for driver allocation

Customer Value Analysis

Aggregate revenue per customer

Recency, frequency, and monetary metrics

CLV segmentation (low / medium / high)

Revenue concentration analysis

SQL Portfolio Analytics

Trips by region & weekday

Revenue per CLV segment

High-value customer distribution

📊 Demand Seasonality
Daily Trips Over Time

Trips by Hour of the Day

Trips by Day of the Week

👤 CLV Analysis
Revenue Share by CLV Segment

Customer segments:

Segment	Description	Revenue Impact
Low	Occasional riders	Low
Medium	Regular riders	Moderate
High (Top 10%)	Most profitable riders	Very high
🗄 SQL Analysis
Trips by Region and Weekday
SELECT 
    region,
    dow,
    COUNT(*) AS trips
FROM trips
GROUP BY region, dow
ORDER BY region, trips DESC;

Revenue by CLV Segment
SELECT 
    clv_segment,
    COUNT(*) AS customers,
    SUM(total_revenue) AS total_revenue,
    AVG(total_revenue) AS avg_revenue
FROM customers
GROUP BY clv_segment
ORDER BY total_revenue DESC;

High-Value Customer Distribution
SELECT 
    t.region,
    COUNT(DISTINCT c.customer_id) AS high_value_customers,
    SUM(c.total_revenue) AS total_revenue
FROM customers c
JOIN trips t
  ON c.customer_id = t.customer_id
WHERE c.clv_segment = 'high'
GROUP BY t.region
ORDER BY total_revenue DESC;

🚀 Key Insights

Clear morning and evening demand peaks

Weekdays significantly outperform weekends in ride volume

A small group of high-CLV customers generates most revenue

Some regions have higher concentration of premium riders

Strong opportunities for targeted retention and pricing strategies

💡 Recommendations

Align driver supply with peak hours to reduce wait times

Build loyalty programs for high & medium CLV customers

Tailor promotions by region and customer value

Expand future analysis with churn prediction & service quality metrics

📁 Repository Structure
demand_seasonality_e_customer_lifetime_value/
├── data/
│   ├── mobility_trips_dataset.csv
│   └── mobility_customers_agg.csv
├── images/
│   ├── daily_trip.png
│   ├── trip_by_hour.png
│   ├── trips_by_dow.png
│   └── clv_segments.png
└── mobility_demand_clv_analysis.ipynb

📬 Contact

Luis Chaumer – Data Analyst
📩 Email: luischaumer@gmail.com

🔗 LinkedIn: https://www.linkedin.com/in/luis-chaumer123
