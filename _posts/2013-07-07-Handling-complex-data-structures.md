--- 
layout: post
title: "Search Engine - Handling complex data structures."
comments: true
tags:
- search
summary: "Complex data strucuture handling in search engines. Denormalization to the rescue."
---

Custom search engines often need to support a variety of entities. Some of them are simple to define, whereas some others are not so straightforward.For any search engine, the most efficient structure for optimal read performance is as flattened as possible. Nested or normalized data structures need to be flattenend.

**Example**

Consider the below structure

    Person
    --Address
    ----ZipCode

If one were to search for all records within a 10 mile radius of a given ZipCode, from a dataset with a few million person records, one can imagine the kind of processing overhead.

Also note that most search engines such as Solr are not relational data-stores. Hence one cannot run SQL like joins to get ad-hoc results. The key is to have all attributes by which one could look up the records, flattened.

Looking at the case of a product vendor (e-commerce), here is an example of an imaginary product's attributes:

    Name
    Brand
    Size
    Price (per size)
    In Stock (per size)
    Manufacturer
    Colour

As a buyer/user, the expectation would be such that the products are easily searchable by name or brand. However, once the user sees a list of matches, he/she could then drill down by choosing the right size, price range as well as colour.

Another implicit filter is availability. The producer would expect to show only those products whose orders can be fulfilled in time.Over and above this, the websites aim to be more interactive, thereby faceted navigation is a key feature.

It has been mentioned earlier that search engine indices are not relational data store. As a result, SQL like data lookup or joins are not available for us to exploit parent-child or normalized data structure. In the case above, availability and price have a many to one relationship with a product.

**De-normalized data**

The way to solve this is to de-normalize/flatten the data. Search engine implementations such as Solr have support for multi-valued attributes, but they need to be one of the primitive types (string etc).

In this case the flattened structure will turn out to be something like this

    Name
    Brand
    Size
    Size_Price
    Size_In_Stock
    Manufacturer
    Colour

One thing to beware is that while flattening, it is best if the duplicates are eliminated. Also, if there is logic involved in flattening, these need to be tested carefully, preferably in isolation. This is because, bad data can lead to false positives. Also [your search is only as good as your data]({% post_url 2012-11-27-your-search-can-be-only-as-good-as-your-data %}).