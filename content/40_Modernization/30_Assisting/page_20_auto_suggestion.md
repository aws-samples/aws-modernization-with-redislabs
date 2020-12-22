---
title: "Auto-Suggestion"
weight: 20
---
Have you ever been frustrated when you know what you’re looking for but can’t quite remember what the term was? Or when you’re faced with a brand new set of documents and you’re not too sure what the critical terms are that provide information in those documents? If the answer is ‘yes’ then this is where auto-suggestion can be a big help.
 
Auto-suggestion gets the computer to do some of the search work for you - you type in some characters and, without you have to do anything else, suggestions as to how those characters match into the underlying information are presented to you. This is a combination of a sophisticated UI and the backend suggestion engine. RediSearch provides that suggestion engine!

To try this out, go to the 'Search -> Autocomplete' page in the application and start typing in the ‘Title’ text box. Type ‘th’ … pretty shortly you’ll see a bunch of selections beginning with ‘Th’ such as ‘The Boy’ and ‘The Fly’ - as you type the suggestion list is modified to better match what you’ve typed. The interactivity is through the magic of javascript which we're not going to go into here, but the underlying suggestions that that javascript serves up come from Redis. 

Let's go to [RedisInsight] and try this out in the CLI:

```
ft.sugget ms:search:suggest:movies th 
```

You’ll get back a list of 4 movies, all beginning with ‘th’. But they’re not in alphabetical order! Why is that? Take a look at the [FT.SUGGET] command and see if you can figure out why the movies are in the order that they’re in! To really understand it you’ll need to look at [FT.SUGADD] too, since that is the command used to put suggestions in a suggestion dictionary.

But how do we know what suggest dictionary to use, or what suggestion dictionaries exist in Redis? in general, there isn’t a command to list the suggestion dictionaries however, in this particular case Tug Grall (the author of this application) named the dictionary well making it relatively easy to find it. Thanks Tug!

In this workshop I found the dictionaries by using the following procedure:

In RedisInsight I selected the Browser, then used the key filter ![key filter icon] to filter on ‘Other module keys’: ![module keys]
 
This gave me a short list of keys: ![short list]

from which I could deduce that `ms:search:suggest:movies` would be of interest.

Exercise: Using the CLI try creating a new suggestion dictionary and adding a few items, then see if you can get suggestions for those items. 

To see this capability in real-life use go to the [Redislabs documentation](https://docs.redislabs.com/latest/rc/) and type in ‘foo’, one letter at a time. After each letter you’ll see a brief list of suggestions based on what you’ve typed in so far. This can help you quickly understand the kind of information that is available to you, and guide you quickly to a productive search experience.

As you can see, indexing and querying, faceted search and auto-suggestion are just a few of the capabilities of RediSearch.  To learn this in more depth you might wish to enrol in the [Redis University RediSearch 2.0 course](https://university.redislabs.com/courses/ru203/). This will really set you up to provide a great experience for your users!


----------
[ft.sugget]: https://oss.redislabs.com/redisearch/Commands.html#ftsugget
[ft.sugadd]: https://oss.redislabs.com/redisearch/Commands.html#ftsugadd
[key filter icon]: filter.png
[module keys]: filter_keys_by_data_type.png
[short list]: keys_short_list.png
[RedisInsight]: http://localhost:8001
