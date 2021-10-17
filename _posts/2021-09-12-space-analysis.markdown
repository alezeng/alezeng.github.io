---
layout: post
title:  "Space Analysis"
date:   2021-09-12 01:04:09 -0700
categories: analysis
---
## Why
In a cloud environment, we have hundreds of thousands of databases to manage. With the understanding of the space usage, we can：
1. Predict the future space requirements
2. Find opportunities to optimize space usage
3. Troubleshooting what unexpected space growth

## How
Goal: **answer any space questions by click on UI**

Design
1. Gather disk/vol level space usage
2. Gather db level space usage
3. Gather tablespace/segment/table level space usage


## What
Implementation
1. Create jobs to gather the space usage and store in a centralize db
2. Create API to show the trend, drilldown and top one with [sql2api framework](/automation/2021/09/06/sql2api-framework.html)
3. Create UI to show the result with [api2ui framework](/automation/2021/09/06/api2ui-framework.html)


*Snapshot example*
![Example](/img/space-analysis.png)
