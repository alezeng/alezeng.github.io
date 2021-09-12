---
layout: post
title:  "Project Tracking Framework"
date:   2021-09-06 01:04:09 -0700
categories: automation
---
# Why
We have many projects going on at the same time. To get the project progress, it takes a lot of time, also data may not accurate if do it manually. We build a project tracking framework based on data provided by API from the source of truth. The framwork will give us the real-time progress and detail, as well as the history trend.

# How
Design:
1. Configurable: add a new project by just adding a new configure
2. Data: get data from configed API which should use data from the source of truth. 
3. Job: setup a daily job to call APIs to collect the data, and store in backend data store
4. UI: build a page to show the current progress of all projects in track, also has a history trend page

# What
1. Configuration: use [dynamic-config] array to configure projects with JSON format value. Example:
{% highlight javascript %}
{
    "project_id": "db_upgrade",     # unique id for the project
    "project_name": "db upgrade",   # display name for the project
    "enable": "true",               # can be used to switch on/off
    "get_data_api": "/common/api/sql2api/get_db_upgrade_status",    # API to get data below
    "comments": "ETA 2021"          # any comments we would like to show on UI
}
{% endhighlight %}

2. API: The API to get data will be vary from project to project. But we will need to have a standard format so the framework can identify it:

{% highlight javascript %}
[{
        "comment": "version 21000",     # anything we would like to explose to UI, could be the value we care
        "item": "db.vip.ebay.com",      # the identity of the item, could be a db vip, or cluster name
        "status": "TBD",                # A few predefined status: TBD, skip, done
        "snapshot_time": "2021-03-03 11:17:51"  # with snapshot time, we know when the data was updated
    },
    ...
]
{% endhighlight %}

3. Job: create a daily job to grab the data for each project, and store current data, and it's history. We can use [data-collector-framework][data-collector-framework].

4. UI:
- A first page bar/column chart page to show the progress of all projects, with a table below to show all the detail items
- Click the bar/column will drilldown to show the history trend of the project progress, with a table below to show only this projects item


[dynamic-config-framework]: /automation/2021/09/06/dynamic-config-framework.html
[data-collector-framework]: /automation/2021/09/06/data-collector-framework.html
