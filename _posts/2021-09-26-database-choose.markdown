---
layout: post
title:  "Database Choose"
date:   2021-09-26 01:04:09 -0700
categories: analysis
---
## Why
It's critical to choose the right database for a given application. 
- If the right db type choosen, it'll be very effcient
- If a wrong db type choose, it'll be endless problems
- There'll be some comprises for operation and db SKU consideration

## How
I will share my options on databases.
### MySQL
 **Pros**
 - Relational, ACID transaction supported
 - Can be cloud native and free of license
 - Active community with multiple solutions

 **Cons**
 - No build-in auto failover, except cluster setup which has limited throughput a lot
 - No build-in sharding support
 
 **IMO**
 - Best choice for small & medium use cases, can support big use cases with well-designed sharding architecture. Can be used for many different cases if well-tuned. For example, as cache KV-store, as Document store using Json data type
 - Not for team without customized architecture/devOps experiences

### Mongo
 **Pros**
 - Document Native support
 - Automated build-in failover mechanism

 **Cons**
 - Community dominated by MongoDB company
 - Only support range sharding
 
 **IMO**
 - Good for small & medium document store use cases
 - Not for high volume or high write required user cases

### Cassandra
 **Pros**
 - Build-in read & write resiliency
 - Write throughput can be very high
 - Adjustable consistent level

 **Cons**
 - Eventual consistency
 
 **IMO**
 - Good for big log user cases 
 - Not for high consistency required user cases

### Couchbase
 **Pros**
 - XDCR: cross cluster/colo sync up 
 - Low latency

 **Cons**
 - Not reliable rebalance mechanism
 - Warm up takes too long
 
 **IMO**
 - Good for distributed KV store use cases
 - Not for critical business user cases

### Foundation DB
 **Pros**
 - Distributed ACID transaction supported database
 - Build-in failover mechanism

 **Cons**
 - Not active community, lack of support
 
 **IMO**
 - Good for distributed transaction required cases
 - Not for critical business user cases

### Oracle
 **Pros**
 - High performance relational DB
 - Good quality product

 **Cons**
 - No build-in cluster/failover for commodity hardware
 - Commercial software, expensive for small business to start

 **IMO**
 - Good for critical business user cases
 - Not the future
