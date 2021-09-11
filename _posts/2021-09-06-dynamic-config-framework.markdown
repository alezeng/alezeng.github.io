---
layout: post
title:  "Dynamic config framework"
date:   2021-09-06 01:04:09 -0700
categories: automation
---
# Why
When we develop systems, it's normal that we will have all kind of different configurations. Some are more static, some are more dynamic in nature. To avoid change code or poke the application to reload the configuration, we need a generic framework to handle configurations to make our configuration dynamic, change on-the-fly.

# How
Design:
1. Configuration type supported: two types of data structure can cover all kind of configuration data: array and dictionary(cover single key-value as well)
2. Most application can consumer data with Json format. So we create generic API to return the data as JSON  
3. Data store design: for each type of configuration, we define 2 tables: one for metadata, one to store value.
4. API: 
    - Array configration: input array_config_name, return an array value in JSON format 
    - Get all value from Dictionary configuration: input dict_config_name, return an array of dictionary in JSON format
    - Get one value for Dictionary configuration: input dict_config_name and key name, return a value of the given key
