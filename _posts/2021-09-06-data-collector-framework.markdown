---
layout: post
title:  "Data Collector Framework"
date:   2021-09-06 08:44:09 -0700
categories: automation
---
Frequently we need to run some data collector jobs, either gather some ad-hoc information. Sometimes we may also want to run it as a job for a while.

# Requirement analysis
In general, there're 3 steps:
 1. Get list of db target to run it
 2. Run the code to get data, most likely in parallel
 3. Store result

# Design
Make it as a standard framework, so people only need to focus on the 2nd step which is the business logic part. Without it, people spend a lot of time on how to run it in parallel with appropriate timeout handling and store the data to a data store for easy usage, either display on a webpage or get by an API.
 1. Create a scheduler. In our case, we use python package *apscheduler*. It can be scheduled a job like crontab or every X seconds. Also, we let it check & reload config every 1 minute.
 2. Let scheduler run the configured job using process/thread pool with a timeout based on config
 3. Have a default function to store the result as json to a data store. We can use MongoDB or MySQL etc.
 4. Create a generic API to get the data from the data store
 5. Create a generic UI to display the current data, and history chart/trend if appliable

We can also use this framework to make changes, store the execution result if you want.

*Snapshot example*
![Example](/img/datacollector-framework.png)

