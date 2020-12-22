---
title: "Redis Caching Benefits"
weight: 30
---
The reduction in latency is the standard use case that most people know Redis for and is Redis' biggest claim to fame. Millions of dollars have been saved by simply using Redis to cache repeated reads that used to always go to large back-end RDBMS systems.

That second benefit - the conservation of resources - is an interesting application of Redis, and leads into a whole area of rate limiting which we won’t get into here, but is well documented [elsewhere]. (This is just one of many use cases where Redis is surprisingly useful, despite being ‘just’ a **RE**mote **DI**ctionary **S**erver.) 

Finally (and we can't really demonstrate this in a simple workshop like this) because Redis is an in-memory datastore it scales very well (linearly, [up to something like 200 _million_ requests per second](https://redislabs.com/blog/redis-enterprise-extends-linear-scalability-200m-ops-sec/)) and the fact that you’ve put Redis in front of OMDB now likewise gives your application massive scale (assuming you're doing a lot of reads compared to writes!). That scale far exceeds what OMDB can do in terms of queries per second while maintaining 1 mS latency. 

So even in the standard caching use case Redis provides a lot of benefit.


----------
[elsewhere]: https://redislabs.com/redis-best-practices/basic-rate-limiting/
