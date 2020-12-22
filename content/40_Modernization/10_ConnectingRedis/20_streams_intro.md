---
title: "Introducing Redis Streams"
weight: 20
---
Let's dive under the covers and see [Redis Streams] through the lens of [RedisInsight].

Go to the Streams section of [RedisInsight]. You will see three streams defined there:

![three-streams]
Make sure ‘Stream Data’ is selected (it should be black) and select any one of the streams. You’ll see a table showing data in that stream along with a timestamp of when each entry was added.

To see the processing side of the stream select ‘Consumer Groups’  at the top. You’ll see that for the movies and actors streams there are active consumer groups, but that the theaters stream has no consumer group. This means that events in the movies and actors streams are being consumed, but that nothing is consuming any event in the theaters stream

A Consumer Group is a set of processing clients that work in parallel to process the events in a stream in an ordered, failure proof and scalable manner. See the [Redis Streams] introduction for more details.

For the inquisitive, when you turned on various services during setup it was services that registered as consumer groups that you were turning on - the consumer groups that would handle the processing of the data from the streams. These services are clients of redis; when an item appears in the stream these services are notified and then they do something relevant to the data and their overall purpose. We'll get into some further details later.

----------
[RedisInsight]: http://localhost:8001
[Redis Streams]: https://redis.io/topics/streams-intro
[Redis Stream]: https://redis.io/topics/streams-intro
[three-streams]: three-streams.png
