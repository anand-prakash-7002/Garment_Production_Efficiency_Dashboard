# Garment Production Efficiency & Delay Analysis Dashboard

## Project Overview
This project analyzes garment manufacturing performance by combining Orders, Production, Inventory, and Dispatch data.  
It identifies factory-level efficiency, stage-wise losses, and production delays, helping stakeholders improve on-time delivery.

## Live Dashboard
**Looker Studio:** <https://lookerstudio.google.com/reporting/05923858-1682-42dc-bfbc-88dda320589f>

## SQL CODE
```SQL
SELECT
    o.Order_ID,
    o.Brand_Name,
    o.Style_Code,
    o.Factory_Name,
    o.Order_Date,
    o.Target_Dispatch_Date,
    o.Order_Qty,
    o.Order_Status,
    p.Cutting_Qty,
    p.Stitching_Qty,
    p.Buttoning_Qty,
    p.Packing_Qty,
    p.Delay_Days,
    ROUND((p.Packing_Qty::decimal / NULLIF(o.Order_Qty,0)) * 100, 2) AS Production_Efficiency,
    ROUND(((p.Cutting_Qty - p.Packing_Qty)::decimal / NULLIF(p.Cutting_Qty,0)) * 100, 2) AS Stage_Drop_Percent,
    EXTRACT(MONTH FROM CAST(p.Production_Date AS DATE)) AS Production_Month,
    EXTRACT(YEAR FROM CAST(p.Production_Date AS DATE)) AS Production_Year
FROM
    orders o
JOIN
    production p
ON
    o.Order_ID = p.Order_ID;
```
## Result 

! 

## Tech Stack
- PostgreSQL / DBeaver (data storage & SQL)
- Google Looker Studio (dashboard)
- Excel (data prep)

## How to run locally
1. Import `Data/Garment_Company_Data_Sample.xlsx` into PostgreSQL or use the SQL file to create tables.
2. Run `SQL/production_efficiency_query.sql` to generate the dashboard dataset.
3. Connect Looker Studio to the resulting table or upload the exported CSV.

## Author
**Anand Prakash** — Data Analyst
