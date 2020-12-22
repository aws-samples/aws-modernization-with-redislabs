---
title: "Connecting"
chapter: true
weight: 10
---
# Connecting From Legacy to Redis
The rules of the game are that our our MySQL database cannot be altered but we want to use Redis to add value to the data in the database. How do we do that?

We will assume we can get some kind of configuration access to our legacy application - this is perfectly normal; configuring the application is in scope; its changing the legacy application that we can't do!

The way this is done here, and would be done in production, is to configure a Change Data Capture (CDC) system with the MySQL database, and to feed its output into Redis as a stream. The reason to use a CDC is because that’s a minimally invasive technology, well understood in the industry, by which any change to some legacy database results in a time ordered sequence of changes being made available externally. Thus loading data into the database, or changing data in the database becomes visible to external systems such as Redis. 

By feeding these changes into Redis Streams they are made available for processing in a variety of ways, which will allow us to implement the requirements [described earlier]({{<ref "40_Modernization" >}}). 

[Redis Streams] provides a robust, durable, ordered communication mechanism whereby stream clients (known as Consumer Groups) can reliably operate on entries of the stream achieving At Least Once semantics. In the rest of the workshop the source of data is a [Redis Stream].

{{% expand "CDC implementation details" %}}
In this workshop we're using a third party CDC system [debezium](https://debezium.io/).  Sufficient to say here that integrating it with MySql and Redis is fundamentally a case of configuration, using the Debezium MySQL connector to listen to events from MySql and to put them in a stream for consumption by Redis. No change to the legacy application; just a matter of installing and configuring an external system.
{{% /expand %}}

----------
[Redis Streams]: https://redis.io/topics/streams-intro
[Redis Stream]: https://redis.io/topics/streams-intro

