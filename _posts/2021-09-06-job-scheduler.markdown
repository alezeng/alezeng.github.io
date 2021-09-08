---
layout: post
title:  "Job scheduler"
date:   2021-09-06 08:44:09 -0700
categories: automation
---
## Why
Once we build automation job with workflow, we can finish a task by submitting a job, for example, upgrade a db. When we have a project to upgrade db, we will need to upgrade hundreds or thousands of databases instances. Do we want to submit job and run it one by one? Absolutely no. We may also don't want to run everything in parallel. We need a job scheduler to orchestrate the jobs, and control the job running scheduler. 

## How
Design:
### When
We need to schedule when to run the job
1. On-demand: it can be handle a urgent situation, we want to submit a job cart(a serlize of jobs) in real time
2. Scheudled: it can be a regular job like cron or run every X seconds, or it can be a planned maintenance that we would like to schedule beforehand

### How to run
The basic question is, do we want to run them in serial, or parallel, or in a small batch. Most cases, we would like to run the jobs in small batch, a controlled parallism.  We define a order number for each job to reach this. The scheduler will run the jobs by the order of the order number.
1. In serial: run it one by one, each job has a unqiue order number. The Job scheduler will kick-off the jobs from lower order number to higher order number.
2. Parallel: every job has the same order number. The Job scheduler will kick-off all the jobs at the same time
3. In group: run as a small batch, need to define a group size. A group say 5 jobs has the same order number, the other group has another order number. The Job scheduler will run the jobs with the same order number in parallel. Only when the lower order number jobs are done, then it can kick off the higher number jobs

### What
We define this Job Scheduler as a framework to support different types of jobs as long as it provide the follow API/functions:
1. Submit a job
2. Update a job status
3. Get a job status
With these, the Job Scheduler will be able to orchestrate the job life-cycle and take appopriate action based on it.
