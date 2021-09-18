---
layout: post
title:  "Data Service"
date:   2021-09-08 01:04:09 -0700
categories: develop
---
## Why
Data Service is a bridge from applications to databases. 

Benefits
1. Easy for applications to access data, hide the complex of the infrastruture. For example, 
   - Merge result from different sharding DBs behind
   - Easy to upgrade drivers without involving applications
2. Build-in Resiliency transparent to applications. For example,
   - Redirect read to cache
   - Redirect traffic from unavailable DB to failover target automatically
   - Mirror traffic for dual write/read
   - Mirror traffic for test


## How
Design
1. Create service pools in every data center, so application can access the service from local data center.
2. Create Logical DB concept. This will hidden physical DB infrasturcture behind. 
3. Build a flexible tool to manage traffic. It should be manage logical DB to physical DB map, and taffic mirror, redirect etc.

