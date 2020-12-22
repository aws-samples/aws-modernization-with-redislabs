---
title: "RediSearch in Action"
weight: 10
---
To see [RediSearch] in action choose the 'Search -> Movies' drop down. You’ll see a page with a search bar containing an asterisk ‘*’, and the results of that search (which, in this case, is all titles or plots matching the wildcard ‘*’. i.e. all movies!).

Type in a search term (say ‘marry’), and you’ll get a list of movies that match the term’s stem, not just an exact string match. 

These kinds of search (and many more) are supported natively by [Redisearch]. It’s very simple to operate, requires no additional purchase, deployment, management or operations, and works at Redis speed. Furthermore developers can stay within their comfort zone of using their current Redis client library - nothing new to learn here; no SQL to get tangled up in; no new libraries to install. Once configured just keep on using Redis the way you always did!



----------
[redisearch]: https://oss.redislabs.com/redisearch/

