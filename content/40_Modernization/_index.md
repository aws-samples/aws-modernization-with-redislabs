---
title: "Modernization"
chapter: true
weight: 40
---
# Modernizing your Legacy Application
The 'Movies (Legacy)' application was written to show the kind of legacy application that so many users have to deal with. The application is just a bare minimum wrapper around the database fields. The application does hide the underlying database schema and associated technology, which is better than nothing, but it offers little further value to the user. 

But what kind of value do we want to bring to the user? We can answer that by looking at how most applications of this kind are used. There are two functions in particular that stand out for most users:

* Finding what you want (i.e you know something in the domain (a movie title, in this instance) and want to find out more about that which, to some extent, you already know)
* Gaining insights (i.e. you want to leverage what you know to tell you things you really didn't know, and which might not even be encoded in the data directly)

In a short while we’ll see how Redis can assist in both of these end-user requirements. 

But first we have another problem to solve: 

We can’t modify the legacy application (that's what we mean by _legacy_). So how do we connect the legacy application (MySQL database in this case) to Redis so that we can use Redis to add value?

----------

