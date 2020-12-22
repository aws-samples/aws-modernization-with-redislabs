---
title: "Caching"
chapter: true
weight: 30
---
# Redis Caching
Redis is known as a cache. Indeed, this is perhaps the main thing that people think about when they hear 'Redis'. But you, dear reader, might not have used Redis as a cache so, for completeness sake, lets work through a simple cache example, using the OMDB web service, so that we're all on the same page when it comes to this basic Redis use case.

{{% notice warning %}}
Spoiler alert: We'll discover that caching can have benefits other than latency, and that this leads into a whole other area that Redis is very well suited for!
{{% /notice %}}


(Of course, if you're already familiar with Redis and caching feel free to skip this lesson!)

