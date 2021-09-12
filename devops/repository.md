---
layout: page
title: "Repository"
permalink: /devops/repository/
---
# DB repository is the source of truth for metadata
Just like we know how much money we have, we need to know how many databases we own. DB respository is a basement of monitor, automation and everything we do about db.

## DB repository for monitor
- If we manually add/remove dbs from monitor, unless you only have a dozen of databases, I'm sure the monitor will be out of data, some db may missing from monitor. 
- Even you can manually maintain the monitor dbs, it's extra efforts and error-prone manually work.
- What I suggest is, use the DB repository as source of truth, and using job/event etc. to automatically add new databases to monitor system, including setup alerts

## DB repository for automation
DB repository can help automation in many ways:
- When we run an automation job, we don't need to input a lot of information but most likely we only need to input the DB vip, the automation infrastructure then using the repository to find all the information needed, such as db version, db role, etc. For example, we would like to switchover a db, we just need to tell the target db vip.
- We can use repository to pre-check and post-check DB cluster layout/health. For example, when we decommission a database, we will check if this is a primary db. If it's, we can pause/stop the job. If it's a secondary copy, we can check if there's other DR target, if there's no other DR target, we also pause/stop as this decommission will cause the primary has no DR which is not valid for the infrastructure. Another example is, after switchover, we can check the repository to find new DR target to check lag, etc.

## DB repository maintenance
- Any manually maintain DB should void.
- Automation job should update DB repository after change. As our automation job will add/remove/change db role, it's important that the job update the repository in time to reflect the truth. This will help us maintain the DB repository as source of truth. 
- Audit DB repository job should be setup. Automation job may run into errors in the middle, that could cause DB repository failed to be updated. We need an audit, even a controlled auto-fix job to fix such unexpected situation. If we use auto-fix, we should carefully evaluate whether it could cause *bad fix* in some cases. If that could happen, we should send that to people to check and then approval auto-fix. This is what we called *controlled automation*. 

