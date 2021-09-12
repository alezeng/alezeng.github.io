---
layout: post
title:  "API to UI Framework"
date:   2021-09-06 08:44:09 -0700
categories: automation
---
## Why
In DevOps work, we need to show data as table or chart with the data we get from API. I've been saw many similiar UI pages like this: a table show the data, and/or a chart which could be different type: pie, column, spine etc. This is duplicated work. So, we came up with the idea to make this a framework. Make it configurable, which is a very important for quick delivery

## How
Design
1. Config an item to generate an UI
2. Configuration
- UI type: could be table, chart, or both. Also, it can be extended to support Form, Sidebar menu, Process Flow
- API: API to get the data. This can use the [SQL to API Framework] [SQL to API Framework]
- API parameters: config the parameters that will be used by the API. This is important to make the page dynamic
- Links: links to other pages. It's very common that we would like to put hyperlinks to connect pages.
- Specific UI configurations: for example, table order column, Chart type, Chart X-axis, Y-axis, time range short cuts which is very common

3. Code
- Call API to get data
- Use modern UI framework like react, vue.js or Angular to render the page

[SQL to API framework]: /automation/2021/09/06/sql2api-framework.html

