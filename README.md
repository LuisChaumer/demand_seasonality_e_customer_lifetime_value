🚕 Mobility Analytics – Demand Seasonality & Customer Lifetime Value (CLV)

Author: Luis Chaumer
Role: Data Analyst
Tools: Python, SQL (SQLite), Pandas, NumPy, Matplotlib
Dataset: Synthetic — 112,568 trips & 30,000 customers
Period Covered: May 2024 → May 2025
Regions: North, South, East, West, Central

📘 Project Overview

This project analyzes passenger demand patterns and customer lifetime value (CLV) for a fictional urban mobility / ride-hailing service.

The analysis performs two key workflows used in real mobility companies:

1️⃣ Demand Forecasting & Seasonality

Analyze hourly, daily, and weekday patterns

Identify peak demand periods

Support fleet allocation & driver scheduling decisions

Explore trends to support forecasting pipelines

2️⃣ Customer Segmentation & CLV

Aggregate customer history: trips, revenue, recency, tenure

Build CLV-style segments (Low / Medium / High Value)

Use SQL to identify high-value regions and revenue concentration

Provide business insights & recommendations

These techniques mimic analytical workflows used by Uber, Lyft, Bolt, FreeNow, and other mobility platforms.

📊 Dataset Description
📂 mobility_trips_dataset.csv

Contains 112,568 trips with fields:

Column	Description
trip_id	Unique trip identifier
customer_id	Unique customer
trip_datetime	Timestamp
region	North / South / East / West / Central
ride_type	Standard / Premium / Pool
distance_km	Trip distance
duration_min	Duration in minutes
price	Final price (incl. surge)
rating	User rating (1–5)
📂 mobility_customers_agg.csv

Aggregated customer-level dataset:

Column	Description
trips	Total trips
total_revenue	Lifetime revenue
avg_price	Average trip spend
first_trip, last_trip	Activity window
recency_days	Days since last trip
tenure_days	Active lifetime
trips_per_month	Frequency metric
clv_segment	Low / Medium / High
📈 Demand Forecasting & Seasonality
Daily Trips Over Time

Clear volume fluctuations across the year with weekly cycles and visible seasonality.

Trips by Hour of Day

Strong morning peak (7–9am)

Strong evening peak (5–8pm)

Midday shoulder periods typical in urban ride-hailing

Trips by Day of Week

Weekdays consistently higher

Weekends show lower core demand with increased leisure trips

🧮 Customer Lifetime Value (CLV)
Revenue Share by CLV Segment

Typical Pareto distribution:

High value customers (~10%) → 50%+ revenue

Medium value customers → strong upsell opportunity

Low value → high volume but low revenue share

🗄 SQL Analysis (SQLite)

SQL is widely used in mobility analytics for dashboards, reporting, and segmentation logic.

🔹 1. Trips by region & weekday
SELECT 
    t.region,
    t.dow,
    COUNT(*) AS trips
FROM (
    SELECT 
        region,
        CASE strftime('%w', trip_datetime)
            WHEN '0' THEN 'Sunday'
            WHEN '1' THEN 'Monday'
            WHEN '2' THEN 'Tuesday'
            WHEN '3' THEN 'Wednesday'
            WHEN '4' THEN 'Thursday'
            WHEN '5' THEN 'Friday'
            WHEN '6' THEN 'Saturday'
        END AS dow
    FROM trips
) t
GROUP BY t.region, t.dow
ORDER BY t.region, trips DESC;

🔹 2. Average revenue by CLV segment
SELECT 
    clv_segment,
    COUNT(*) AS customers,
    ROUND(AVG(total_revenue), 2) AS avg_revenue,
    SUM(total_revenue) AS total_revenue
FROM customers
GROUP BY clv_segment
ORDER BY total_revenue DESC;

🔹 3. High-value customers by region
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

🚀 Insights & Business Recommendations
🔍 Key Findings

Strong intra-day peaks → ideal for driver scheduling automation

Weekday/weekend differences imply different service patterns

High-value riders are concentrated in a few key regions

Revenue is heavily influenced by a small high CLV population

🔧 Recommendations

Optimize driver supply around demand peaks to lower wait times.

Create loyalty tiers or rewards for medium & high CLV customers.

Use CLV segments for marketing audience targeting.

Expand this analysis with churn prediction & cancellation metrics.

Develop region-level incentives for premium riders.

🧰 Tech Stack

Python: Pandas, NumPy, Matplotlib

SQL: SQLite

Jupyter Notebook

Time Series Analysis + Segmentation

📁 Repository Structure
mobility-demand-clv-analysis/
├── data/
│   ├── mobility_trips_dataset.csv
│   └── mobility_customers_agg.csv
├── images/
│   ├── daily_trips.png
│   ├── trips_by_hour.png
│   ├── trips_by_dow.png
│   └── clv_segments.png
├── mobility_demand_clv_analysis.ipynb
└── README.md

📬 Contact

Luis Chaumer
Data Analyst
📩 Email: luischaumer@gmail.com

🔗 LinkedIn: www.linkedin.com/in/luis-chaumer123
