---
layout: post
title:  "Dynamic Config Framework"
date:   2021-09-06 01:04:09 -0700
categories: automation
---
## Why
When we develop systems, we will have all kind of different configurations. With a framework to manage these configurations, having these benefits:
- Reduce the work of build frameworks which can use it whenever needed
- Change configurations on-the-fly, no code change or rollout
- Make create-monitor-item-in-1-day and add-automation-job-in-1-week possible

## How
Goal: make all configuration dynamic configurable. 

Design
1. Configuration type supported: two types of data structure can cover all kind of configuration data: array and dictionary (cover single key-value as well)
2. Most application can consumer data with Json format. So, we create generic API to return the data as JSON  
3. Data store design: for each type of configuration, we define 2 tables: one for metadata, one to store value.
4. API: 
    - Array configuration: input array name, return an array value in JSON format 
    - Get all value from Dictionary configuration: input dictionary name, return an array of dictionary in JSON format
    - Get one value for Dictionary configuration: input dictionary name and key name, return a value of the given key

