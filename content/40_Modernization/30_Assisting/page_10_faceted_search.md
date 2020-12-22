---
title: "Faceted Search"
weight: 10
---
What 'faceted search' provides is a means for uses to interact with 'facets' or 'attributes' of data which have a defined range of values. In our movie case obvious facets are 

* Release Year
* Ratings
* Genre

If you select the 'Movies (Faceted)' from the search drop down menu you’ll see a page which allows you to experience how a UI artifact (in this case, sliders for ‘Release Year’ and ‘Ratings’; select boxes for ‘Genre’) can make a faceted search seem very natural. 

![faceted-search]

The fact that it's using search at all is rather hidden from the users, but leveraging the indexes and using the underlying query mechanisms is exactly what’s happening!

You’ll see the corresponding search expressions on the page (that’s just an artifact for our pedagogical purposes - you wouldn’t normally expose this to end users!).

```
FT.SEARCH ms:search:index:movies " @release_year:[1990 2010] @rating:[5 10] "
```

This searches for movies whose release year is in the range 1990 thru' 2010 inclusive, and whose rating is between 5 and 10 inclusive. By changing the sliders on the left, or clicking on the 'Genre' boxes, you can alter the search dynamically, in real time. The search expression is likewise altered.

Lets try those search expressions out natively! Take the above search expression and execute it in the CLI in RedisInsight and see what you get.


Digging into the syntax by looking at the documentation for the [FT.SEARCH] query syntax you’ll see that the ‘@’ symbol prefixes a field (here we have release_year and rating), and the ‘[ … ]’ syntax denotes a numeric range (in this case 1990 to 2010, and 5 to 10) inclusive by default. 

Try modifying the search to get a feel for how this works. How about the years 1980 to 1985, inclusive? How about 1981 to 1985 - can you search for that range using both an inclusive and an _exclusive_ search?

By now you should be starting to realize that RediSearch provides some pretty powerful capabilities, all built into Redis, and working at Redis speeds (i.e. native C). 


----------
[faceted-search]: faceted-search.png
[FT.SEARCH]: https://oss.redislabs.com/redisearch/Commands.html#ftsearch

