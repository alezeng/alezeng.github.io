---
layout: post
title:  "Job Cart Framework"
date:   2021-09-06 08:44:09 -0700
categories: automation
---
## Why
Once we build automation job with workflow, we can finish a task by submitting a job, for example, upgrade a db. When we have a project to upgrade DB, we will need to upgrade hundreds or thousands of databases instances. Do we want to submit job and run it one by one? Absolutely no. We may also don't want to run everything in parallel. We need a job cart to orchestrate the jobs and control the job running cart. 

## How
Design
### When
We need to schedule when to run jobs
1. On-demand: it can be handled a urgent situation, we want to submit a job cart (a series of jobs) in real time
2. Scheduled: it can be a regular job like crontab or run every X seconds, or it can be a planned maintenance that we would like to schedule beforehand

### How to run
The basic question is, do we want to run them in serial, or parallel, or in a small batch. Most cases, we would like to run the jobs in small batch, a controlled papalism.  We define an order number for each job to reach this. The cart will run the jobs by the order of the order number.
1. In serial: run it one by one, each job has a unqiue order number. The Job cart will kick-off the jobs from lower order number to higher order number.
2. Parallel: every job has the same order number. The Job cart will kick-off all the jobs at the same time
3. In group: run as a small batch, need to define a group size. A group say 5 jobs has the same order number; the other group has another order number. The Job cart will run the jobs with the same order number in parallel. Only when the lower order number jobs are done, then it can kick off the higher number jobs

## What
We define this Job Cart as a framework to support different types of jobs as long as it provides the follow API/functions:
1. Submit a job
2. Update a job status
3. Get a job status
With these, the Job Cart will be able to orchestrate the job life cycle and take appopriate action based on it.

*Snapshot example*
![Example](/img/job-cart.png)