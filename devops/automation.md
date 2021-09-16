---
layout: page
title: "Automation"
permalink: /devops/automation/
---
## Why
### Save lazy people
Human is lazy by natural. It's just like why we create washing machine. It gives people more time to do creative things.
### Improve availability
We used to have human errors caused impact to db availability every year. From shutdown the wrong database to delete the wrong files, exectute command at the wrong window. As human, we make mistakes, that's nature, we've to accept the fact. How to solve this delima? My thought is, do not let people do it. Then who will do it? Automation. So, we setup automation jobs for all kinds of *dangerous* works. 
## How 
### How to avoid automation make mistakes
As we all known, automation will make mistakes, that's what we called *bugs* in code, or unexpected situation to the code. In my past experiences, I didn't have a single instance that let automation cause bad damage. How do we reach that? 
- Pre-check is must for any automation. Pre-check is to check the pre-requirements. If the pre-requirement is not met, then don't start the auto-job at all. That will avoid unexpected situation.
- Make sure every step exits with the right return code. This is critical to avoid *silent failure*. This is critical for any automation. If there's any failure, must be captured and reported. If it's fatal or unexpected result, the auto-job should rollback, or pause, or stop, or report to people as appopriately. 
- Post-check is also must for any automation. Post-check is to make sure the situation is what we expected after our auto-job. This will help us find any potential issue. Instead of waiting for monitor system to alert it, or even customers to report issues, we can find the issue immediately, and then fix it at the first time, greatly reduce the time to recovery.

## What
### Automation framework
As the tech work is changing very violently. The new features/requirements are kept coming. Our infrastructure also needs to response quickly. My goal is to setup automation job in 1 week. To reach that,
- Build things like logo, we need to build small blocks (basic libs/objects, for example, a db instance), compound functional blocks (a business logic, for example, bounce a db)
- Build/use a configurable workflow system: by using the previous blocks to build an end-to-end automation job, for example, patch a database.
- If we cannot reach the goal a build a job in 1 week, review the previous two steps, we need to improve them in some extents.

[automation framework blog](/automation/2021/09/05/automation-framework.html)