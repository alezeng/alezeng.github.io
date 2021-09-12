---
layout: post
title:  "SQL to API framework"
date:   2021-09-06 08:44:09 -0700
categories: automation
---
## Why
In DevOps work, we need to get data in format like Json while most our data is stored in data store. I've been saw many APIs are similar: write a query to query DB and format the data as Json to return. This is duplicated work. So, we came up with the idea to make this a framework. Make it configurable, which is a very important for quick delivery

## How
Design
1. Config an item to generate an API
2. Configuration
- Data source Type: support frequently used data stores like MySQL, MongoDB, Oracle, etc.
- Data source: can be predefined or configured in real-time
- Query: a query to get the data 
- Bind Variables: this is an important! This makes our configured API can accept parameters
3. Code
- Generate connection based on the defined Datasource
- Run the Query using Bind Variables if any
- Format result to Json and return


