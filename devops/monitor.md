---
layout: page
title: "Monitor"
permalink: /devops/monitor/
---
# Auto discovery for monitor
As we are managing hundreds of thousands of databases, create and decomm databases are normal. Monitor must be setup with auto discovery. In simple, when a new database created, it should be automatically monitored. To reach that, 
- DB needs to have a repository/metadata, which is the source of truth. 
- Monitor infrastructure needs to auto discovery, by jobs or events to get db repo, add new databases to monitor and remove decommed database from monitor.

# Alert for monitor
- The reason why we setup monitor? One the most important reason is, know there's a problem before customer report. We don't want to watch, also cannot watch every item 7*24. So have an alert is very important, otherwise the monitor item will be only FYI, or for post-morterm check.

# Suppress for monitor 
- Either monitor or alert, it would be there's a known issue or outliner. If we kept get alerts on such cases, people will get bored/tired of these alerts, then ignore it, then probably could miss other real monitor alerts. That will be a big problem. So have a way to suppress monitor/alert is important, we also need to set a timeline when that suppress will be expired. 

# Framework for monitor
Monitor is critical for DB systems. Without monitor in place, we cannot say we're production ready. My goal is to setup any monitor metrics in 1 day, better in 1 hour. To reach that,
- Have a monitor framework in place is essential, such as Prometheus.
- Have a framework to gather metrics. To add a metric to the framework, it could be adding a configure/SQL, or a small piece of function/code to get the metric. We also need auto job to release the change to all dbs if it's agent-based framework, such as Prometheus exporter.
- Auto/easy push the metrics to monitor framework. It should be done automatically or simple config change, also importantly we should be able to customize the threshold, alert methods etc. 
- If we cannot reach the goal to add a monitor in 1 day, review the previous two steps, we need to improve them in some extents.

