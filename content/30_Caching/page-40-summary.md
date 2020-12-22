---
title: "Caching Summary"
weight: 40
---
We showed how a slow (web) service ([OMDB]) can benefit from using Redis as a cache when the service is slow or has access restrictions. You experimented with turning caching on and off and saw how the presence or absence of a cache had a marked effect on latency and api usage.

We've finished with OMDB now. Let’s move on and use a MySQL database as your movie data store to consider some more ways Redis can help modernize your application.


----------
[OMDB]: https://omdbapi.com
