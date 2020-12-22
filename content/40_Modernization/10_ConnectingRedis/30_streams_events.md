---
title: "Generating Events in Redis Streams"
weight: 30
---
Let's generate some change events and see what happens. We’ll update a movie, and see how that is reflected in the stream.

Go back to viewing the ‘Stream Data’ for the ‘movies’ stream.

On the right hand side select ‘View Columns’ and ensure that only the 'source.operation’ 'release_year' columns are displayed, and that the table is sorted by timestamp with the latest timestamp at the top (do that by clicking on the timestamp column header until you've got the desired sort order). Your table should now look something like the following:

![movies-stream]

You can see that the stream has a lot of 'create' events - this is how Redis was populated in the first place; by listening in as records were created in MySQL during startup and having these records placed in the stream by the CDC system.

Now, in the 'Movies (Legacy) application' click on ‘Guardians of the Galaxy’, change the Release Year from 2014 to 2020 and Submit the change. 

Go back to [RedisInsight]/Streams and you’ll see that the first row of the table has changed to reflect this update (if you’re quick you’ll actually see the update happen before your eyes!). You should see an 'update' record, like this;

![movies-updated]


----------
[movies-stream]: movies-stream.png
[Redisinsight]: https://localhost:8001
[movies-updated]: movies-updated.png

