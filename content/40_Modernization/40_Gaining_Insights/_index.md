---
title: "Gaining Insights"
chapter: true
weight: 40
---
# Gaining Insights
The interfaces we’ve seen so far go a long way toward modernizing the application and adding value to the end user. Those users can now list movies, search them, get assisted in their search. But those are the first level of queries that users have about data. The next level is really about relationships between data items. Queries like ‘What were the movies that the actors who worked with Tom Cruise worked on, that Tom Cruise himself didn’t work on’ (that’s hard to write, never mind hard to figure out how to say that in SQL!)

For this Graph Databases have proved to be far more expressive than standard relational databases. No surprise then that Redis includes a graph capability,  [RedisGraph]! So, graph capabilities at the in-memory speeds of Redis! [RedisGraph] implements a subset of the [Cypher] language, which is growing as development continues. This document is based on the [Cypher Query Language Reference (version 9)][cypher], available at [OpenCypher Resources].


----------
[redisgraph]: https://redislabs.com/modules/redis-graph/
[cypher]: https://s3.amazonaws.com/artifacts.opencypher.org/openCypher9.pdf
[opencypherresources]: https://www.opencypher.org/resources
[redisinsight]: http://localhost:8001
[first tom query]: first_tom_query.png
[second tom query]: second_tom_query.png

