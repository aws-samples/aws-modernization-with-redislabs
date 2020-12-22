---
menuTitle: "Introduction"
chapter: true
weight: 10
---
# Solving Data Challenges in Cloud Applications with Redis

Welcome to the Solving Data Challenges with Redis workshop. We're glad you're here and sharing some of your precious time with us! We hope you'll find this valuable and will come away with a deeper appreciation of how to solve these challenges using Redis, as well as a strong idea that there's more to Redis than we're telling you about!

So what's so special about Cloud Applications? Well, they're ubiquitous, and becoming more so with the Covid pandemic. The whole going online program has been accelerated by several years, as [evidenced by this report from BDO]. But more than that, they have unique data challenges:

- Very low latency
- Very large number of users
- High Scalability
- High availability
- Intense competition (rapid application development)

There are many solutions that address some of these challenges, but few that really address them all and at the scale required. It turns out that Redis is such a solution that was specifically created to address exactly this market, and has successfully proved itself for over a decade. Which is why we're talking to you about it as a solution!

Redis has been primarily used as an in-memory, NO-SQL cache where it is amongst the fastest in its field (with less than 1mS latency) and (in the [Redis Labs Enterprise] commercial offering) has shown itself [capable of scaling out] to handle _hundreds of millions_ of operations per second at that latency, in highly available architectures.

All that is well and good, but more is required to really solve the data challenges. In particular the intense competition amongst online providers is increasing, and this requires that cloud applications:

- be developed and deployed rapidly
- be repurposed quickly
- meet the ever-increasing and demanding user expectations effectively and efficiently

all while meeting the latency, scale and availability. 

So this goes beyond simple caching and into the architecture and data realm, starting with how to develop on a developer's laptop to how to architect using micro-services so that application developers can leverage previous work and not re-invent, re-deploy or re-manage what is already known to work. It also goes into the actual user experience, and the support for advanced data management features that can be exposed directly to the user. 

As you go through this workshop you'll be exposed to not just the simple caching use-case (which we cover for completeness' sake), but to other use cases as described above. We'll introduce the use case and the issue, and then show how features of Redis can be used to solve the issue. 




--------
[evidenced by this report from BDO]: https://www.bdo.com/insights/business-financial-advisory/strategy,-technology-transformation/covid-19-is-accelerating-the-rise-of-the-digital-e
[Redis Labs Enterprise]: https://redislabs.com/redis-enterprise/advantages/
[capable of scaling out]: https://redislabs.com/blog/redis-enterprise-extends-linear-scalability-200m-ops-sec/
