--- 
layout: post
title: "Search Engine - Index v/s Query time boosting"
comments: true
tags:
- search
summary: "Some points on index vs query time boosting."
---

Boosting is a way in which the fields are ordered in priority. By default all fields defined in the search engine schema are of the same priority (or weights). However, often there are cases where match against one field is more evident than others.

One of the goals of the search engine is to reduce noise and thus have most relevant results surface, boosting plays an important role when there are contention. However, like many other features, a small mistake in boosting could have multiplicative effect on the search results. It is worth spending some time analyzing the need for boosting.

**Index time boosting**

There are often cases where the key attributes of an indexed entity are evident. The name of a product, the title of an article etc are examples of attributes that most users will look for. These attributes naturally outweigh some of the other attributes of an entity. For instance, the name of a product is more important than the country of manufacture, when searching for the product. Hence while indexing these attributes can be boosted, so that even the simplest search can benefit from this.

**Query time boosting**

While there are a few attributes that are prominent in a product, the rest are often not easily ranked in the order of how relevant they are to the user. In this case, any boosting that gets applied could be dependent on the context in which it is searched for. Query time boosting helps create a query that contains the field boosts that is relevant to the given context.

**What to choose**

Index time boosting can become quite impractical as most of the user scenarios expect some context in which the search needs to adapt. Also, the performance implication of query time boosting isn't very much when compared to index time boosting. I, personally, have used query time boosting for all my scenarios and it scaled pretty well.

**_Using both is not such a good idea_**

One thing to beware of is that the idea of doing both Index and Query time boosting is very tempting, but it is not trivial to decide fields that can be boosted at index time. Very often there are conditions coming in, and it then gets trickier. Also, if query time weight has to offset index time boosts (happens when context overrides the default behaviour), it is again additional logic.

**_Context awareness_**

In order to give to the most relevant results, context awareness is very crucial. It doesn't have to be a personalized mechanism, but just
understanding something in the lines of the facets applied could lead to various ways in which the weights need to be tuned. A few example:

Case 1 = User searches for 'Sony'

Now, Sony is a big brand in Electronics. So if the search results for all electronics get boosted, it will probably be the most relevant result set. There might be an edge case where let's say accessories for an electronic equipment is tied to the brand.

Case 2 = User searches for 'Nokia'

While both Sony and Nokia manufacture cellphones, Nokia do just that. They are known as a cellphone company. Hence, this now needs to go beyond electronics, and go to Electronics->Cellphones.