---
title: "Conclusion"
weight: 50
---
In this workshop you have:

* Examined how basic Redis Caching can add value to an external application
* Used [RedisInsight] to interact directly with Redis
* Learned about more sophisticated use of [Redis Streams] and CDC
* Discovered that [RediSearch] is the gateway to really enhancing your application, making it much more interesting and useful to your users
* Had a brief taste of [RedisGraph] and the powerful [Cypher] language

But this is only the beginning. Redis can do much more! For example:

* Redis can count very [large numbers of distinct items in constant space] (great for determining if a user has every logged in before, or if an IP address has ever been used before); 
* Redis can provide [synchronous messaging] between clients (think of game servers, each serving thousands of users, but needing to rapidly send messages about user's status etc. from one server to another)
* Redis can [implement leaderboards] very efficiently; something that SQL really struggles to do!
* Redis supports [geospatial] indexes, so you can easily provide sophisticated mapping interfaces to users

These are just a few of the many features of Redis that often go unknown and unappreciated. I hope that this workshop has persuaded you to think more about Redis and maybe consider looking it at as so much more than a cache!

If you like what you see but are interested in a higher performance, more scalable, more secure and optionally managed Redis then why not [register for Redis Enterprise] and get 30 days free access to a 4 node cluster to really see what Redis can do!

----------
[Redisinsight]: https://redislabs.com/redis-enterprise/redis-insight/
[redis streams]: https://redis.io/topics/streams-intro
[redisearch]: https://oss.redislabs.com/redisearch/
[large numbers of distinct items in constant space]: https://redislabs.com/redis-best-practices/counting/hyperloglog/
[synchronous messaging]: https://redis.io/topics/pubsub
[implement leaderboards]: https://redislabs.com/solutions/use-cases/leaderboards/
[geospatial]: https://redislabs.com/redis-best-practices/indexing-patterns/geospatial/
[redisgraph]: https://redislabs.com/modules/redis-graph/
[cypher]: https://s3.amazonaws.com/artifacts.opencypher.org/openCypher9.pdf
[register for Redis Enterprise]: https://app.redislabs.com/#/login
