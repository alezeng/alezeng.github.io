---
layout: post
title:  "Monitor Framework"
date:   2021-09-06 08:44:09 -0700
categories: monitor
---
## Why
There's a lot of open-source monitor framework. We also used some of them like prometheus/grafana. They're awesome for time seried metrics.
However, some are not time series metrics, such as capacity which could be a current status. We need to have home-growned specific monitor for them.

## How
Design
 1. Gather data. It can use the [job cart framework] [job cart framework]
 2. Get data by API. It can use the [SQL to API framework] [SQL to API framework]. One important thing is that the data should be based on metadata. If a DB didn't have metrics, that should also be reported.
 3. Setup monitor by configuration

## What
 1. Setup a monitor UI using configuration: metrics threshold, stale threshold, link to history data, 
 2. Send alerts if there's out of threshold or stale
 3. Alert if the data is stale

[job cart framework]: /automation/2021/09/06/job-cart-framework.html
[SQL to API framework]: /automation/2021/09/06/sql2api-framework.html

