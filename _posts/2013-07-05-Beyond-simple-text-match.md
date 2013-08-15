--- 
layout: post
title: "Search Engine - Beyond simple text match"
comments: true
tags:
- search
summary: "Describes various scenarios where custom search engine implementations can go way beyond simple text match."
---

When using a search engine, a lot of use cases would be looking up an entity. It could be either searching for a user, a product or something similar. In such cases, there is a good chance that the user might enter a query phrase that would bring up exactly what he/she is looking for.

However, in the rest of the use cases, the users wouldn't enter a phrase query that brings up exactly what he/she wants. This could or could't be intentional. There are cases where entering a very accurate search phrase would yield less than desired results. Ex - while shopping for footwear or apparels, the users are less likely to have the exact make and brand in mind. Rather, the search phrase would be generic enough to get results that allows users to compare brands, promotions, price ranges etc.

There is also the other side, where we have a catalog of products, that the user isn't familiar with. It would be highly improbable that the users would enter something like the Product Id, although this does happen.

In summary, the search engine needs to scale across this wide set of requirements. Hence there is often a need to go beyond simple text match or lookup. And most search engine tools offer plugins/ features to do these operations.

There are two aspects of implementation that helps us achieve this.

**Indexing** - While importing data into the search engine, it helps if there is some analysis done to understand what kind of a field would be a natural fit. There are Tokenizers and Analyzers that play a big role in defining the characteristics of an indexed field and these can be exploited to match the expected results. For instance, in Lucene, a Standard Analyzer with Whitespace tokenizer would index every word in the field. NGram filter would enable the field to be looked up by part of the words as well.

**Querying** - Indexing helps when a field can be designed without the query context. However, there could be multiple use cases on the same field, the logic depends heavily on the query phrase and context. In such cases, Solr helps by providing a good amount of options to perform lookup. (Description of Solr query syntax can be found in the documentation).   

###A few examples where there is a need to go beyond Simple Text match:

**_Range Query_**

These queries fetch results that fall within the range of a given field values. A user could fetch all documents that have price between 100 and 200, for example.

**_Aggregate Query_**

These queries use an aggregated value. An example would be to get the cheapest blue shirt from multiple brands.

**_Conditional Query_**

As the name suggests, this uses a boolean flag to determine whether to match a document or not. Stock availability check would be a typical example.

**_Weights_**

When there is a search term that is ambiguous, there is often a choice to be made across fields. For example, "Surface" could be a part of description of physical attribute (ex - reflective surface), but is also a product by [Microsoft]([http://www.microsoft.com/surface/](http://www.microsoft.com/surface/)). Hence it becomes important that when in conflict, there is a way to resolve them.

One way is to assign weights to the fields, so that they get prioritized. Sometimes, the weights could be at index time, where the relative priority of the attribute can be defined at the schema definition level. But often, the context makes a huge impact on this, and hence the weights (or boosts) can be given at the query time.

**_function query_**

This feature allows queries to contain functions that get evaluated against every document to match hits.

**_dynamic fields_**

This feature allows search engines (Solr) to have fields assigned to document at runtime, thus givin great flexibility on attributes that can get associated to a document.

**_Multi lingual_**

The search engines can be localized and contain terms from multiple languages. Having a single instance cater to multiple languages can have an implication as same term can have additional complexity of interpreting language.

User's locale come in handy to resolve probable language that the user would be interested in, but this requires additional logic.

**_date time_**

As with languages, localization can have currency and date time complexity. Formats of dates vary foe each locale and can lead to ambiguity.

This can be mitigated by resolving all request to a standard timezone.

**_geo spatial_**

Search engines also come with geo-spatial support, which allows ones to search for local entities for a user. This is a powerful feature, expecially when visualizing results on a map.
