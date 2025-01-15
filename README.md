# Carbon Emissions by Industry

## Overview
This project analyzes the carbon footprint of various industries using the `product_emissions` dataset. By focusing on the most recent year, it identifies the number of unique companies and their total carbon footprint (PCF) for each industry group. Results are ranked to highlight the most impactful sectors.

## Key Query
The query performs the following steps:
1. Identifies the most recent year using `MAX(year)`.
2. Aggregates data by `industry_group` to calculate:
   - Number of unique companies (`num_companies`).
   - Total carbon footprint (`total_industry_footprint`), rounded to one decimal.
3. Sorts industries by their total carbon footprint in descending order.

## Sample Query
```sql
SELECT industry_group,
       COUNT(DISTINCT company) AS num_companies,
       ROUND(SUM(carbon_footprint_pcf), 1) AS total_industry_footprint
FROM product_emissions
WHERE year IN (SELECT MAX(year) FROM product_emissions)
GROUP BY industry_group
ORDER BY total_industry_footprint DESC;
