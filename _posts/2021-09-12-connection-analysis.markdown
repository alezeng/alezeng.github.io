---
layout: post
title:  "Connection Analysis"
date:   2021-09-12 01:04:09 -0700
categories: analysis
---
## Why
In a cloud environment, we have thousands of applications, and hundreds of thousands of clients. With the understanding of the connections pattern, we can：
1. Have a clear picture of which application used how many connections in history and real-time
2. Find opportunities to optimize from application connection
3. Troubleshooting issues caused by connection

## How
Goal: **answer any connection questions by click on UI**

Design
1. Gather real time connection by application & db
2. Aggregate data to get daily peak connection
3. Compare DB connections by given two different time, show the changes on application level
4. Compare Two DB connections, show the differences on application level
5. Analysis a DB connection trend
6. Analysis an application connection trend on a given DB
    
## What
Implementation
1. Create a real-time job to gather real-time connections with application information
2. Create a daily job to aggerate the daily data
4. Create API to analysis the data with [sql2api framework](/automation/2021/09/06/sql2api-framework.html)
5. Create UI to show the data with [api2ui framework](/automation/2021/09/06/api2ui-framework.html)

