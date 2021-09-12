---
layout: post
title:  "Traffic Analysis"
date:   2021-09-06 01:04:09 -0700
categories: analysis
---
## Why
In a cloud environment, we have thousands of applications, and hundreds of thousands of clients. With the understanding of the traffic pattern, we can：
1. Predict capacity based on traffic trend.
2. Find opportunities to optimize from application traffic 
3. Troubleshooting issues caused by traffic

## How
Goal: **answer any traffic questions by click on UI**

Design
1. Tracking traffic: This could be from application log or tracking system. we've 1 trillion calls per day,
2. Aggregate data: 
- Aggregate the data with these dimensions: application, SQL, DB, day. This will reduce the data vol is 10M+ per day.
- Aggregate for drilldown: 
    application -> DB -> SQL
    application -> SQL -> DB
    DB -> Application -> SQL    
    DB -> SQL -> Application
- Aggregate for trend: for each of the drilldown level above, we will be able to show the trend
    
## What
Implementation
1. Gather application logs
2. Use Hadoop to analysis daily log to generate the first level aggregated daily data
3. Load Hadoop result to database, and aggregate for drilldown & trend, save to cubic tables
4. Create API to analysis the traffic with [sql2api framework](/automation/2021/09/06/sql2api-framework.html)
5. Create UI to show the traffic with [api2ui framework](/automation/2021/09/06/api2ui-framework.html)

