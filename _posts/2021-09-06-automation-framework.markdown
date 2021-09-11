---
layout: post
title:  "Automation Framework"
date:   2021-09-06 08:44:09 -0700
categories: automation
---
Requirement of automation framework
1. There's no best, but the most suitable one. 
- We don't need to have the best one, it may need a lot more time/invest which impact the ROI.
- The suitable one is the one that meet the business requirement with minimum invest. Think about this like you are running a business.

2. Flexible enough
- Configurable steps, so we can build end-to-end automated business flow like lego, reuse existing steps or workflow
- Manual steps support. It's a journey to get fully automated, before we can get everything automated, we may still need to people to execute some steps, for example 3rd party action which didn't have appopriate API, or approve an action which need human's judgement.
- Each step exit code should be accurately handled. This is important for reliablity of the job.
- Input parameters should be configurable, and as less as possible, using the metadata repository to get what needed as much as possible.
- UI should be auto-generated based on configuration
- Logs should be easy to access at real time. It will be easy for use to get the detail and troubleshooting.
- Provide a mechnisam for parameters or result transport between steps 
- Concurreny control: sometimes operations are mutual exclusive or we want to limit the concurrency of rollout
- Workflow/parallel control: we may need to run multiple steps at the same time, and then merge the workflow
- Security control: automation is a sharp tool, it can hurt if not well controlled, security is one of the most important control

