---
layout: page
title: "Architecture"
permalink: /devops/architecture/
---
## Why
### Availability is by design
Everything will fail in some ways at some time. Since failure is un-avoidable. The design will decide how reliable the system is, how resiliency it will be. 

### Scalability is by design
How we setup the DB and application will decide how we can scale out infrastructure. For example, if we sharded it, we will be able to scale out with the shard logic later. If we didn't, then we can only scale up with more powerful hardware. We all know that no matter how powerful a machine is, it has a limit. While scale out is more easy and cost efficiency normally.

## How
### Read resiliency
It's normal that 99%+ time application are reading from DB, no write operation. For example, view a page, it will read only. Having read resiliency is the critical for users experiences too.

### Write resiliency
Write is mostly the customer action. For example, place a order, pay the bill, etc. This is normally the source of revenue. It's not as frequently as read, but it's more important

### Sharding
The data volume was growth expoenentially in the mobile internet era. It's important to design our applications/DBs to be able to support the business/data growth if it happens. 

## What
### Read resiliency
1. `Use cache`: cache is quick, and cache can be easily extended normally. It can be persistent cache or non-persistent cache per requirements. Such as memcached, couchbase, Redis, Oracle timesten etc.
2. `Use secondary copy`: read from secondaries. Many DB has secondary copies, such as MySQL, PostgreSQL, MongoDB. With apporpriate application set up, they can read 

Caution: every cache or secondary copy will have some extented lag, application needs to be take that in consideration, check if business can torelarent with it.

### Write resiliency
1. `DB cluster write resiliency`: some DB has such feature. For example, Cassandra(Quorum based write, Hinted Handoff), Oracle RAC. But many DB didn't have such build-in features.
2. `Write to another store and sync back`: build a failover DB store, and let application write there temporiraly in case of main DB failure, and have a mechnism(such as Kafaka) to sync it back to the main DB.

### Sharding
The main choice we need to make is the shard logic:
1. `Range based sharding` 
- Pros: good for range based data; extend linearly
- Cons: limited to specific data type; not evely distributed data may cause hot range; split range is heavy operation

2. `Hash based sharding`
- Pros: any data type; can be distributed evenly
- Cons: cannot serve range query efficiently; extend only with 2X capacity

3. `List based sharding`
Similiar to Range
- Pros: simple and straightforward; extend linearly
- Cons: limited to data/key with be high uniqueness; not evely distributed data may cause hot range; cannot split the for a list value

4. `Metadata based sharding`
We can store the data map data in a metadata table. Applications will ready the map data first, and then go to the real shard. For example, use zonekeeper to store the map data.
- Pros: flexible; easy to split range; can support both range-based sharding, hash-based sharding or list-based sharding
- Cons: need maintain high read availablity of the map data; extra hop to get the real data, can be remedy by using cache in some extents;


