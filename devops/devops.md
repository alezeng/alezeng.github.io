---
layout: page
title: "DevOps"
permalink: /devops/
---
# My Experiences
I have been intensively worked on DB Ops and Dev in the last 10+ years. I was lucky enough to involved in running *one of the largest e-commercial* site in the world. We've been supported **1 trillion** calls per day with 99.994% availability for 5+ years. One year we reached 99.999% availability which means 5 minutes downtime in a year. We have only about 30 teammates to support 10000 database instances. The rate is about 300 DB per person. I would like to share some best practices that I think make this happen.

# Overall
In my opinion, these aspects impact the availability the most: architecture, monitor and automation. 
Think about your work like you are running your own business.
## Architecture
The setup of DB and Application is the basement of how reliable the site will be. 
- DB deployment architecture: whether we shard the DB, how many datacenters we deploy them, how do we do disaster recovery, etc.
- Application architecture: how application resiliency to write failure? How application resiliency to read failure?
- Kept POC new things: this is how we keep our stack/architecture up to the front of the technical world.

## Monitor
- Monitor things that matters
There's endless of metrics that we can monitor, find the most meaningful and business impacted metrics to monitor only
- Alert is needed for important metrics.
If a metric is monitored but didn't setup alert, then it may not be noticed even when it's bad. We cannot rely on people to manually watch it every day.
- Alert needs to have a way to suppress for a period
Alert can be caused by planned maintenance or known issues that are solving in progress. If we cannot suppress it, then people will get bored and overloaded with the alerts, then real important alerts may be ignored.
- Setup flexible monitor workflow/framework 
If there's a requirement to monitor a metric, my goal is to setup it in the *one day*, with end-to-end coverage on all DBs and alter setup. 

## Automation
Automation is an important part for high availability. As human will make mistakes which is normal even for senior person, also we cannot guarantee every person we hired are senior. The benefit of a person cannot be aggregated or duplicated. But automation/code can be improved overtime steadily. It helps us reduce human error to near zero. We don't need people to execute any risk tasks, such as change table structure, shutdown, decommission DB. In most cases, we don't even need people to logon to the host or database.  
- Automation any repeat work with priority
Same to monitor, there's endless works can be automated, and we always have limited time, so prioritize is very important. That will improve your ROI.
- Setup flexible automation workflow/framework 
If there's a requirement to automate a task, my goal is to setup it in *one week*. If we cannot reach that, that means we need to improve our framework, or need more basic libs to make it easier.


