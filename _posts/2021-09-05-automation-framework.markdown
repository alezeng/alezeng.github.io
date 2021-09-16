---
layout: post
title:  "Automation Framework"
date:   2021-09-05 08:44:09 -0700
categories: automation
---
## Why
There's a lot of open-source automation framework, for example, Airflow.
However, we have some old scripts which was not easy to model to match the requirements. So, we created a home-growned automation workflow and add specific features that we need.

## How
Design
- **Configurable steps**: we can build end-to-end automated business flow like Lego, reuse existing steps or workflow
- **Manual steps support**: it's a journey to get fully automated, before we can get everything automated, we may still need to people to execute some steps. For example, 3rd party action which didn't have appropriate API, or approve an action which need human's judgement.
- **Restartable steps support**: when there's a failure in workflow, whether we can restart/resume the job, this should be definable.
- **Appropriate exit code**: this is important for reliability of the job.
- **Configurable input parameters**: this provides the flexibility, also make it as less as possible, using the metadata repository to get what needed. It can also be used to verify the input parameters.
- **Auto-generated UI**: based on configuration
- **Real-time status and logs**: help get detail and troubleshooting.
- **Save/transport middle result mechanism**: it's common the latter steps need to use previous step result 
- **Concurrency control**: sometimes operations are mutual exclusive, or we want to limit the concurrency of rollout
- **Workflow/parallel control**: we may need to run multiple steps at the same time, and then merge the workflow
- **Security control**: automation is a sharp tool, it can hurt if not well controlled, security is one of the most important control

## What
1. We use DB tables to store the data for the automation framework:
- Job category table: used to group jobs in UI
- Job metadata table: store job info like name, maximum concurrency etc.
- Job step metadata table: store step info like where to run, how to run, what command/script/api to run, manual step or restartable etc.
- Job and Job step map table: store the map and order of steps of jobs
- Job parameter table: it will define and store the input parameters of jobs
- Job log table: store job instance log
- Step log table: store step instance log

2. Define jobs from UI
- It will add items to the tables above except logs table which is used by real-time instance.

3. Submit jobs from UI
- User will need to input the parameter values defined which will be stored in job log table as input parameters

4. Job agents pick up jobs and run it
- Job agents will pull the jobs/steps to be run
- Replace parameters in brace like {parameter_name} with user-input or previous steps injected values
- Run the step as step meta defined. If a middle result needs to be used afterwards, inject the values to the job log table
- Repeat above until all steps are done


