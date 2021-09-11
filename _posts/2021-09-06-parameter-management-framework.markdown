---
layout: post
title:  "Parameter Management Framework"
date:   2021-09-06 01:04:09 -0700
categories: automation
---
## Why
We manage hundreds of thousands of databases. The hardware and software are evolving all the time. Even though we are trying to make it a uniform environment. During the transition/upgrading process, it will be a hybrid/mixed environment with different hardware and software version. The db environment is very sensitive to parameters. It's a lot of work and error-prone if manually manage it. So, we setup a rule based parameter management framework. We only need to define the rules, and the framework will make sure the parameters following the rule.

## How
Design:
1. Define dependencies: which fact will impact parameters
- The metadata of dependency will be column from metadata. For example hardware SKU, software version, db family
- The value of dependency will be the value of the specific fact. For example hardware G1.
2. Define rules connection with dependencies: while rule apply to which dependencies. For example, set a rule user_G1_family for user family db uses hardware G1.
3. Define parameters of rules: which parameter-value pairs should be setup for which rule. For example, set db cache memory to 100G and parallisim to 8 for user_G1_family
4. Define base and rule priority
- Define a base rule with all default parameters
- Each rule has a priority number, base rule will have the lowest priority
- If a parameter was defined by mutliple rules, the parameter value of higher priority rule will win
 

## What
Implement logic overview:
1. Get parameters based on rule
- Input: the metadata of a db, it will include all the facts such as hardware type, db version, family, vip, etc.
- Calculate parameters by rules priority
- Output: parameter-value pairs
2. Compare parameters with live/setting value
3. Change the live/setting values

The core logic is *Calculate parameters by rules priority*:
1. Get each rules dependencies. For example:
{% highlight javascript %}
-- rule1
{
    'hardware': 'G1'
}
-- rule2
{
    'hardware': 'G1',
    'family': 'caty'
    ...
}
{% endhighlight %}

2. Use the db's metadata to match defined dependencies to see if there's a match. For example, 
{% highlight javascript %}
-- meta data
{
    'hardware': 'G1',
    'family': 'user'
    ...
}
-- It will match rule1, but not rule2. 
Bascially we test if the rule dependency dictionary are in metadata dictionary. 
In python3, we can use this test:
if rule1.items() <= dbmeta.items()
{% endhighlight %}
Order the matched rules by priority, and add base rule which has the lower priority.

3. Get all the parameters of matched rules. If a paramter in multiple rules, the win value is the value from rule with highest priority.
