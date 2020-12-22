---
menuTitle: RedisInsight
weight: 20
---

### RedisInsight
[RedisInsight] is a great tool for interacting directly with Redis. You'll be using it extensively during this workshop to understand what Redis is doing for the application 'under the covers'. You'd normally install this locally on your laptop or similar where you might manage multiple databases, but this isn't so much a class about RedisInsight as a class about what Redis can do for you, so we've installed a RedisInsight service and now we need to get you connected to it!

First, in your Cloudformation Outputs page click on the 'RedisInsightsUrl' link, and (after a minute or so) you should see the End User License Agreement Page:

![db0 eula]

Toggle the 'I have read and understood the RedisInsight License Terms' and then hit 'CONFIRM'. You'll be taken to the Welcome screen:

![db1 connect]

Choose the 'I already have a database' button to take you to the first configuration screen:

![db2 configure]

Then choose the 'Connect to a Redis Database' button where you can add the redis database using the 'Host', 'Port' and 'Name' field values from your Cloudformation Outputs page:

![db3 configure]

Click on 'Add Redis Database' to finish.

You'll end up at a window looking like this:

![db4 created]

Click on the 'redis-service' database and you'll get to the actual database interaction window:

![redis-service]

{{% notice tip %}}
Whenever we direct you to [RedisInsight](https://redislabs.com/redis-enterprise/redis-insight/) throughout the rest of the course this is the window you'll need to go to. We'll be directing you to various menu options shown on the left hand side of this window. Best to open this up in another tab now and keep it open for use later!
{{% /notice %}}

----------
[redis-service]: redis-service.png
[RedisInsight]: https://redislabs.com/redis-enterprise/redis-insight/
[db0 eula]: db0-eula.png
[db1 connect]: db1-connect.png
[db2 configure]: db2-configure.png
[db3 configure]: db3-configure.png
[db4 created]: db4-created.png
