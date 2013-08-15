--- 
layout: post
title: "Implementing Search Engine - Defining fields and weights"
comments: true
tags:
- search
summary: "How to work out and decide on the list and type of fields with their weights."
---

There is much more to implementing a search engine than wiring up data sources. Often the search result are heterogeneous in definition. Again, looking at the e-commerce vendor's case, the objective of the search engine could be to list products that match the search criteria.

In this case, it is quite common for a vendor to be providing multiple types of products, hence the search results need to list multiple product types. The heterogeneous nature of the entity does not stop at just search results, in fact this is an important consideration for defining the schema of a search engine.

**Identifying fields**

A search engine is agnostic to the domain, and treats entities by the text/values it's attributes hold. Hence, it is important to analyze the fields of a product that are relevant to a search engine. It is worth noting that the search engine fields need to be driven by the way a user would look at a product, not as a vendor or implementor.

For instance, a product could have the below fields

  * Name
  * Size
  * Expiry
  * Manufacturer (Brand)
  * Price

Out of the above fields, the user would probably search by Name and Brand. Additionally the user may filter the results by price (range) and size. However, the Expiry field is something that the user may not search by or filter. It is however an important attribute for the vendor to track. Thus, in this case, the search engine field definition could be complete by including just the Name, Size, Brand and Price fields.

By this point, the search engine would be capable of giving matching products to a query.

**Identifying Priority of relevance**

There can be a good number of cases where the search criteria is quite vague and there are more than one correct way of listing the results. There could be multiple reasons to this, there could be many products with same Brand and query is by Brand name or there could be match across fields.

Although search engine logic can be fuzzy, the same search against the same data set should yield in the same result set. In order to eliminate the randomness that emerge due to conflicting matches, search engines can have weights.

Weights help decide the priority of matches when a query matches across fields. Ex - Name could have the first priority, i.e when a query has conflicts with two products when the match of one product is on the Name and the other is on say, Brand, the search engine weights could decide that the Name match is more relevant than Brand match.

**Defining weights**

Most search engines provide an easy way of defining weights in the fields, however it takes a fair bit of analysis to understand the right order of priority across fields.

In Lucene based search engines (Solr or Elasticsearch), one could define the weights by applying relevant boosts to the fields.

It is also worth noting that seasonal events and spikes could influence the priority of the fields. For instance, if a vendor is running promotion on a particular brand, it could be the case such that the Brand field takes priority over Name, so that the products under promotion could reach the users better.

[Index v/s querytime boosting]({% post_url 2013-07-09-index-vs-querytime-boosting %}) discusses more about boosts.

**Identifying Field Type**

Most search engines come with the ability to define various data types for the fields. This helps in doing operations that are relevant to the data in place. For instance, text comparison can be done on strings, arithmetic operations on numbers etc. This helps in performing search beyond simple text match. This post talks about performing search [beyond simple text match]({% post_url 2013-07-05-Beyond-simple-text-match %})

**Indexed v/s Stored fields**

Of all the attributes that have been identified for a product, there are two categories. One set of fields are those which can be used to look-up a product. Another category are attributes that define a product and are key for the user to identify the product, but are not searched by. The advantage of storing fields in the search engine is that once the product record is identified using the indexed fields, the next step, which is displaying the results, can be fulfilled completely using stored values. This saves a call per product list to the primary datastore. The magnitude of gain is even more when looking at a normalized datastore.