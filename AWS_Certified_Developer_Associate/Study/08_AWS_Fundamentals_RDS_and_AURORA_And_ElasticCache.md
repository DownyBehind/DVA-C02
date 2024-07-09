# AWS Fundamentals RDS + AURORA + ElastiCache

## ElastiCache

ElastiCache

ElastiCche Overview

The same way RDS is to get managed Relational Databases
ElastiCache is to get managed Redis or Memcached

Caches are in-memory databases with really high performance, low latecy

Helps reduce load off of databases for read intensive workloads

Cache miss 난 경우에는 DB로 가서 읽는다.
그리고 Cache에 읽은 값을 쓴다.
다음에는 Cache hit가 된다.

ElasiCache - Redis vs Memcached

Redis

- Multi AZ with Auto-Failover
- Read Replicas to scale reads and have high availability
- Data Durability using AOF persistence
- Backup and restore features
- Supports Sets and Sorted Sets

Memcached

- Multi-node for partitioning of data(sharding)
- No high availability (replication)
- Non persistent
- No back up and restore

Caching Implementation Considerations

Is it safe to cache data?
: Data may be out of date, eventually consistent

Is caching effective for that data?
: Pattern: data changing slowly, few keys are frequently needed
Anti Pattern: data changing rapidly, all large key space frequently needed

Is data structured weel for caching?
: example: key value caching, or caching of aggregations results

Which caching design pattern is the most approproate?

Lazy Loading / Cache-Aside / Lazy Population

- 강의 자료 참조

장점
:

- Only requested data is cached (the cache isn't filled up with unused data)
- Node failures are not fatal (just increased latency to warm the cache)

단점
:

- Cache miss penalty that results in 3 round trips, noticeable delay for that request
- Stale data: data can be updated in the database and outdated in the cache

Write Through - Add or Update cache when database is updated

- 강의 자료 참조

장점
:

- Data in cache is never stale, reads are quick
- Write penalty vs Read penalty(each write requires 2 calls)

단점
:

- Missing Data until it is added / updated in the DB.
  Mitigation is to implement Lazy Loading strategy as well
- Cache churn - a lot of the data will never be read

Cache Evictions and Time-to-live(TTL)

- Cache eviction can occur in three ways:

* You delete the item explicitly in the cache
* Item is evicted because the memory is full and it's not recently used (LRU - Least Recently Used)
* You set an item time-to-live (or TTL)
