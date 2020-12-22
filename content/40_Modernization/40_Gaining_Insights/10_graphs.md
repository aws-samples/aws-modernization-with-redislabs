---
title: "Redis Graph"
weight: 10
---
So, let's get to work! [RedisInsight] provides a great RedisGraph interface. Open it up and let's try a little Cypher!

First query: let's find the actors that have acted with Tom Cruise. The Cypher expression is:

```cypher
MATCH (tom:actor{last_name:'Cruise'}) - [:acted_in] -> (m:movie) <- [:acted_in] - (a:actor) return m, a
```

Let’s talk about the graphs and then dissect the query above: Graphs consist of nodes, and relationships between the nodes. You can think of a node as something containing data, and a relationship as connecting the nodes. A graph database allows one to rapidly trace some set of relationships to gather the nodes that are of interest.

Cypher is a pattern oriented language - here the nodes in the graph (actors, movies) are represented in parentheses, and the relationships between are shown in square brackets with lines and arrows to show direction (Cypher does support undirected relationships too). So we can see that the 'tom' node is related to some movie 'm', because tom acted in that move. Likewise we can see that there is an actor 'a' that likewise acted in movie 'm'. And the query returns both 'm' and 'a'. In this case both 'm' and 'a' are not necessarily a single pair; Cypher will use this general pattern to find all nodes that match this general pattern (including the original 'tom' node!).

This should return a result like the following (assuming you’ve got the graph viewer selected): ![first tom query]

(note how Tom is the highly connected actor (green circle) in the middle)

Hovering over a node will select it, and show more information in the bottom left. Double clicking it will expand any relationships and redraw the graph. I’ll let you spend time trying that out - its very intuitive!

So, from the above graph, we can easily see that no actor worked on more than one of Tom’s movies. I wonder why?

So let's extend the query a bit more - let’s take those actors and figure out what movies they worked on that Tom Cruise didn’t work on. In SQL this starts to get harder to express, and the combinatorial complexity rapidly increases, slowing down processing. This is where the expressive power of the Cypher language comes into play, and the graph optimized processing from RedisGraph results in good performance.

The Cypher query is:
```
MATCH (tom:actor{last_name:'Cruise'})-[:acted_in]->(tm:movie) <- [:acted_in] - (not_tom:actor) -[:acted_in] -> (ntm)
where not_tom.last_name <> 'Cruise'
AND tm <> ntm 
RETURN ntm,not_tom
```
You can interpret the Cypher above as traversing the relationship from tom through to movies tom has acted in (tm) through actors that aren’t tom (not_tom) to movies that tom has not acted in (ntm). Note the use of the Where clause to ensure that tom and his movies are excluded from the results.

This looks like: ![second tom query]

from which we can deduce that some actors that had worked with Tom got to work on multiple movies that he didn’t work on. This is hard to figure out with SQL and tabular representations, but pretty easy from a graph perspective.

Try to figure out the Cypher expressions for these queries:

Easy: Did Tom Cruise and Emily Blunt ever work on the same movie? If so, which one?
{{% expand "Answer:" %}}
Yes, Tom and Emily did work together, on 'Edge of Tomorrow'.

Here's the query:
```
match (tom:actor{last_name: "Cruise"}) -[:acted_in]->(m:movie) <-[:acted_in]-(e:actor{last_name:"Blunt"}) return m
```
{{% /expand %}}

A little harder: Which movie had the oldest actors, and what was their average age?

{{% expand "Answer:" %}}
The movie Vincent had actors whose age averaged 71 at the time of release.

```
match (a:actor) -[] - (m:movie) return avg(m.year - a.dob) as age, m.title order by age desc limit 1
```
{{% /expand %}}


----------
[redisgraph]: https://redislabs.com/modules/redis-graph/
[cypher]: https://s3.amazonaws.com/artifacts.opencypher.org/openCypher9.pdf
[opencypherresources]: https://www.opencypher.org/resources
[redisinsight]: http://localhost:8001
[first tom query]: first_tom_query.png
[second tom query]: second_tom_query.png
