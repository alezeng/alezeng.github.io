---
layout: post
title:  "Monitor Framework"
date:   2021-09-06 08:44:09 -0700
categories: monitor
---
There's a lot of open source monitor framework. We also used some of them like prometheus/grafana. They're awesome for time seried metrics.
However, there're some non time seriezed metrics, such as capacity which could be a current status. We need to have home-growned specific monitor for them.

# Requirement analysis
In general, there're 3 steps:
 1. Gather data. It can use the [routing job framework][routing job framework]
 2. Get data by API. It can use the [SQL to API framework][SQL to API framework]. One important thing is that, the data should be based on metadata. If a DB didn't have metrics, that should also be reported.
 3. Setup monitor by configuration

# Design
 1. Setup a monitor UI using configration: metrics threshold, stale threshold, link to history data, 
 2. Send alerts if there's out of threshold or stale
 3. Alert if the data is stale


[routing job framework]: /automation/2021/09/06/routing-job-framework.html
[SQL to API framework]: /automation/2021/09/06/sql2api-framework.html