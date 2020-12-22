---
menuTitle: "Application"
weight: 10
---
## Example Application
The example application is the Redis Movie Database. Its a simple database application with Movies as the underlying application domain. The ideas here are applicable to a wide range of domains and, hopefully, what you see and experience will help you see where you too can use Redis to enhance your users access to data.

Using this application you'll be able to understand:

- How to improve both the latency of, and access to, an external service using caching;
- How to modernize a legacy application by:
  - Using [Redis Streams] to capture data changes
  - Making it easy to find what you want
  - Assisting users in real time
  - Gaining new insights

Purely for teaching purposes we’re going to have two data sources:

1. The first is an external web service, OMDB, that provides data about movies, albeit relatively slowly (a latency of 150mS or so), and with access limits (1,000 requests a day to the API). This is a useful vehicle to show the caching story. 
2. The second data source is a local MySQL database many of whose movies originated from OMDB (although not all). Our story here is where the modernization aspect of using Redis really takes off. 

{{% notice warning %}}
The system you have access to comprises a MySQL database, a Redis database and an application. We haven’t tested every path through this combination of technologies, so it is entirely possible that you might break things as you try some things out, although hopefully only when you’re exploring on your own, and not when you’re following the instructions! But you can simply stop and restart everything and you should be good to go!
{{% /notice %}}

----------
[redis streams]: https://redis.io/topics/streams-intro
