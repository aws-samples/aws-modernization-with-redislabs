---
title: "Search under the covers"
weight: 20
---
Let's look under the covers and get to grips with search using [RedisInsight]

In [RedisInsight] select ‘RediSearch’ on the left hand side. At the top on the middle right use the drop down menu to select the `ms:search:index:movies` index:

![redisearch-indices]

These indexes were created by the application - we’ll dig into them more shortly.

To execute a search similar to the ‘Search’ page you saw earlier, type ‘marry’ in the search query bar and hit return.

You’ll see the actual underlying redis command (`FT.SEARCH ms:search:index:movies marry`)  that was run, and the results. (Read the [FT.SEARCH] documentation for details.)

{{% notice warning %}}
The 1.7.1 version of [Redisinsight] has a bug: it appends an extra colon to the end of the index name. If you look carefully you'll see that the command is shown as:

```
FT.SEARCH ms:search:index:movies: marry
```

You'll have to correct this when you use the CLI and remove the additional colon, thus:

```
FT.SEARCH ms:search:index:movies marry
```

{{% /notice %}}

Now copy that command to the Redis CLI (you’ll find that in [RedisInsight] as a menu item on the left hand side), paste it in and run it there to see the raw output. You should see something that starts like this:

```
>> FT.SEARCH ms:search:index:movies marry
 1) (integer) 12
 2) "ms:docs:movies:990"
 3)  1) "release_year"
     2) "2019"
     3) "poster"
     4) "https://m.media-amazon.com/images/M/MV5BNjU2NDllZjEtZjFkZC00ZDlhLWE3MjktY2RiYTU0NjY3NGYzXkEyXkFqcGdeQXVyMTQxNzMzNDI@._V1_SX300.jpg"
     5) "plot"
     6) "This new series expands the fan-favorite Married to Medicine to the West Coast. In the city of glitz and glam, these doctors save lives by day and walk red carpets at night. The docuseries ..."
     7) "movie_id"
     8) "990"
     9) "genre"
    10) "Reality-TV"
    11) "rating"
    12) "4.099999904632568"
    13) "votes"
    14) "34"
    15) "title"
    16) "Married to Medicine: Los Angeles"
 4) "ms:docs:movies:903"
 5)  1) "release_year"
     2) "1981"
     3) "poster"
     4) "https://m.media-amazon.com/images/M/MV5BZjQzZDlhNWMtZDBlMS00YTgxLThiZDctNDA2N2EyZjNlMjE3XkEyXkFqcGdeQXVyNDEzNTUxMTk@._V1_SX300.jpg"
     5) "plot"
     6) "Story of Texas heiress Joan Robinson, who married plastic surgeon John Hill. Her father, Ash, is suspicious of Hill, thinking that he married Joan for money, which he used to buy a house ..."
```

All well and good, but as anyone who knows search knows, it's all about the indices. Where are they? What do they look like? How were they created? How are they populated?

We’ll take those questions in reverse order: One of the great things about RediSearch is that the index population and maintenance is fast (Redis speeds, remember!) and automatic - you simply define the key patterns that have values you want to index and the index will be maintained as values are created, updated or deleted on keys matching that pattern. Its that easy! 

{{% notice note %}} At this time the only things that can be indexed are Redis Hashes. This might sound like a big limitation but in practice it's not a problem. It turns out that for the structures where search is most often used then the native data structure is a hash, or the data is easily represented by a hash. 
{{% /notice %}}

So when we went to the ‘Search -> Movies’ page how was the index that supports that page populated? In a real-life application there’d be a once only export from the legacy system (MySQL in this case) followed by an import into Redis. What we do here in the Workshop is simply create both the MySQL and the Redis systems (including index creation, described below)  and then process any changes written to the streams, creating, updating and deleting entries as required. Specifically, the Consumer Group ‘cdc.search.index’ is the stream client which processes changes to generate the indexes according to the operation for that change. 

So now we know how indices are populated, but how are indices created in the first place?

An index is created using the [FT.CREATE] command. In that command one indicates the search schema - this schema defines:

- The key prefixes whose values are to be indexed
- The structure or attributes of the items that will be indexed,
- and the ways that the index will use the values. 

For example, it describes the type of certain attributes; whether those attributes are sortable or not; the weight to be given to those attributes.  

We’re not going to dive into the details here of creating an index, but will instead learn how to find out more about already created indices using the [FT.INFO] command. Let’s look at the `ms:search:index:movies` index.

Using the CLI within [RedisInsight] execute the following:

```
ft.info ms:search:index:movies
```
You should get the following output:

```sh
>> ft.info ms:search:index:movies
 1) "index_name"
 2) "ms:search:index:movies"
 3) "index_options"
 4) (empty list or set)
 5) "index_definition"
 6)  1) "key_type"
     2) "HASH"
     3) "prefixes"
     4) 1) "ms:docs:movies:"
     5) "language_field"
     6) "__language"
     7) "default_score"
     8) "1"
     9) "score_field"
    10) "__score"
    11) "payload_field"
    12) "__payload"
 7) "fields"
 8) 1) 1) "title"
       2) "type"
       3) "TEXT"
       4) "WEIGHT"
       5) "5"
    2) 1) "plot"
       2) "type"
       3) "TEXT"
       4) "WEIGHT"
       5) "1"
       6) "SORTABLE"
```
(Your output will be much longer - we've truncated it here for clarity).

In standard Redis command response syntax the result is a numerically labeled and nested attribute/value list, with the attribute name being immediately before the corresponding value. So, for example, line 1) defines the attribute name `index name`, and line 2) its value `ms:search:index:movies`

Given that brief outline, we can see that the index definition is at position 5, and comprises 6 sub attributes. We can see that attribute 6) 3) indicates the following attribute contains `prefixes` of keys with which this index will be automatically populated. Attribute 6) 4) is thus an attribute list, albeit a list of only length 1 in this case. Attribute 6) 4) 1) is the `ms:docs:movies` prefix. 

So, hopefully, you can now understand that the `ms:search:index:movies` will  be populated with any hash whose key has a prefix of `ms:docs:movies`.

Quick question for you: how many prefixes can a RediSearch index have? 1 exactly, more than 1? Is there a limit? Go check out the RediSearch documentation and see what you can figure out!

So now you know how indices are created, and populated, the question is, where are they kept? 

{{% notice note %}}
In RediSearch 1.0 the indices were regular Redis key/value pairs, but in RediSearch 2.0 they became hidden inside Redis itself. This was done to enable various further technical features to be added. 
{{% /notice %}}

To see indexing in action, lets update a movie:

In the CLI, take a look at the movie with ID 7:

```
hgetall ms:docs:movies:7 
```

You’ll see that the movie title is 'X-Men: Days of Future Past’. There is no plot field - lets add one:

```
hset ms:docs:movies:7 “Film about some angry X-Men”
```

If we now search for the string ‘angry’ you’ll see that that plot line matches the search, and the hit is against that specific movie.

Exercise: Go look at the movie stream and see the change in that stream.

As you have experienced, once indexing is set up index management is completely automated, leaving the developer and users free to concentrate on the core use case to which these features can be applied.

----------
[FT.SEARCH]: https://oss.redislabs.com/redisearch/Commands/#ftsearch
[FT.CREATE]: https://oss.redislabs.com/redisearch/Commands/#ftcreate
[FT.INFO]: https://oss.redislabs.com/redisearch/Commands/#ftinfo
[RedisInsight]: http://localhost:8001
[redisearch-indices]: redisearch-indices.png
