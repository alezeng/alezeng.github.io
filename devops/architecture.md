---
layout: page
title: "Architecture"
permalink: /devops/architecture/
---
## Why
### Availability is by design
Everything will fail in some ways at some time. Since failure is un-avoidable. The design will decide how reliable the system is, how resiliency it will be. 

### Scalability is by design
How we setup the DB and application will decide how we can scale out infrastructure. For example, if we sharded it, we will be able to scale out with the shard logic later. If we didn't, then we can only scale up with more powerful hardware. We all know that no matter how powerful a machine is, it has a limit. While scale out is easier and cost efficiency normally.

## How
### Read resiliency
It's normal that 99%+ time applications are reading from DB, no write operation. For example, view a page, it will read only. Having read resiliency is the critical for users experiences too.

### Write resiliency
Write is mostly the customer action. For example, place an order, pay the bill, etc. This is normally the source of revenue. It's not as frequently as read, but it's more important

### Sharding
The data volume was growth exponentially in the mobile internet era. It's important to design our applications/DBs to be able to support the business/data growth if it happens. 

## What
### Read resiliency
1. `Use cache`: cache is quick, and cache can be easily extended normally. It can be persistent cache or non-persistent cache per requirements. Such as Memcached, Couchbase, Redis, Oracle timesten etc.
2. `Use secondary copy`: read from secondaries. Many DB has secondary copies, such as MySQL, PostgreSQL, MongoDB. With appropriate application set up, they can read 

Caution: every cache or secondary copy will have some lag, application needs to be taken that in consideration, check if business can tolerant with it.

### Write resiliency
1. `DB cluster write resiliency`: some DB has such feature. For example, Cassandra (Quorum based write, Hinted Handoff), Oracle RAC. But many DB didn't have such build-in features.
2. `Write to another shard`: for sharded DB type, write to another shard is also an option. For example, Mod shared DB, Mod based on sequence, each shard has different seq ending. The sequence is generated at insert data time, and application doesn't care which share it write to, just need to get the sequence number back, then it will know which shard it is.
3. `Write to another store and sync back`: build a failover DB store, and let application write there temporarily in case of main DB failure, and have a mechanism (such as Kafka) to sync it back to the main DB.

### Sharding
The main choice we need to make is the shard logic:
1. `Range based sharding` 
- Pros: good for range-based data; extend linearly
- Cons: limited to specific data type; not evely distributed data may cause hot range; split range is heavy operation

2. `Hash based sharding`. The simplest hash method is Mod. 
- Pros: any data type; can be distributed evenly
- Cons: cannot serve range query efficiently; cannot extend linearly; need to migrate/split data when extend

3. `List based sharding`
Similiar to Range
- Pros: simple and straightforward; extend linearly
- Cons: limited to data/key with be high uniqueness; not evenly distributed data may cause hot range; cannot split the for a list value

4. `Metadata based sharding`
We can store the data map data in a metadata table. Applications will ready the map data first, and then go to the real shard. For example, use zone keeper to store the map data.
- Pros: flexible; easy to split range; can support both range-based sharding, hash-based sharding or list-based sharding
- Cons: need maintain high read availability of the map data; extra hop to get the real data, can be remedy by using cache in some extents
