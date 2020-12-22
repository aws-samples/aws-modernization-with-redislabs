---
title: "Turning on Caching"
weight: 20
---
So lets turn on caching!

In our application we've made it so you can turn caching on and off simply by operating the slider where it says 'Redis Cache' under the movies on the 'Movies (Legacy)' page.

If the slider is white then caching is off:

![caching-off]

If the slider is blue then caching is on:

![caching-on]

With caching **off** hit the refresh button a couple of times and observe whatever latency you get (could be as low as 60mS, or as high as several hundred; it all depends on your network). You'll also see that each time you hit the refresh button the API count goes up - you're consuming those precious resources!

Now turn caching **on**, and hit the refresh button **ONCE** only. You'll see little to no change in the latency figure, and you'll see that the API count has increased. 

Hit the refresh button again, as many times as you like. You should see two things:

* Firstly, the latency has dropped dramatically to 0 or 1mS - that's very quick!
* Secondly, you're no longer consuming those precious API calls!


You might like to think about the above behavior a bit and try to figure out why, after turning caching on:

1. The initial latency figure didn't change much after the firt click, while the API count increased;
2. The latency then dropped to near zero, and the API count stop increasing.

----------
[caching-off]: caching-off.png
[caching-on]: caching-on.png

