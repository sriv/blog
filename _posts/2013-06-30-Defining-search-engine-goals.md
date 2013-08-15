--- 
layout: post
title: "Search Engine - Defining Goals"
comments: true
tags:
- search
summary: "Some goals that can be tracked in order to keep track of search engine implementation."
---

Once the needs have been identified, it is time to define some metrics and create benchmarks. By nature, search can be quite subjective and fluid. There are a variety of plugins that can change the behaviour of the search engine by applying various algorithms. Some of these algorithms are [fuzzy](http://en.wikipedia.org/wiki/Fuzzy_logic)

Hence it is important that there are enough parameters that help decide whether the search formula in place is as expected. This can be done by co-relating metrics that would get affected by the search engine's performance. Some examples are illustrated below.

###Direct Metrics

####Click-through ratio (CTR)

This metric identifies the ratio of visits that have successful search result to the total number of searches. The success of search could be defined as expected user action post performing the search (ex- open the links in the result).

A benchmark of this metric could help understand how many users are dissatisfied with the search results. Any significant improvement of this metric could mean the Search Engine is providing the users whatever they are looking for.

####Number of "No results found"

This metric can be a measure of "failure" scenarios, i.e. the search engine failed to deliver what the user was looking for. But this metric in it's raw form can be misleading. There are a few reasons why this would happen:
a) The user is looking for a product/content that doesn't exist
b) Misspelled search terms or Invalid search criteria
c) Genuine search issues, where user has the right input and the product/content that the user is expecting for actually exists.

(a) and (b) are cases that can be filtered out as they are out of the search engine's control. However in case of (c) there can be two reasons again - (i) the product/resource have been not tagged correctly or have incomplete metadata, and (ii) the search engine is configured incompletely or improperly.

Case (ii) above would be direct feedback to the search engine, whereas (i) will be feedback to the owner of data.


####Average user duration in search
This metric reflects the amount of time a user spends in a search result page. Depending on what the user does next, this could be a measure of satisfaction or dis-satisfaction of the user. 

Duration Length \Outcome|Success|Failure
---|---	|---
Short|Good Search results, good UX on result screen|Poor search results
Long|Good Search results, UX on screen can be improved|Poor search results, Poor UX|

The success and failure definition is the same as defined above in CTR section. The user experience of search result page is important too. The last thing you would want is good results which the users can't see!

####Statistics on refining search
These metrics help quantify the search engine's performance in every scenarios.

**refinement ratio**

This is a measure of the amount of tweaking and tuning of search criteria that the user needs to do to get to where she wants to be.

**drill up/drill down clicks**

This is a measure of how accurately the level of display is. Sometimes the search results are too general and some other times they are too specific. Both cases are extreme unless the user enters a criteria that general or specific.

**facet hot-spots**

This is a measure of what across all content/products are most users concentrating. There are a wide range of inferences this can yield, but again these are specific to the business.


###Indirect Metrics

####Sales trend

This is again assuming an e-commerce setup. A good search strategy can boost sales, either by surfacing popular products in the right relevance or by bringing out niche products. In either case, there could be multiple reasons for such a boost and the influence of search can only be inferred, subjectively. 

####Cross selling trends

A lot of e-commerce vendors try to use strategy such as surfacing related products, or bundling one product with another. the motivation could vary - in certain cases a symbiotic relationship boosts up other products as popular products sales increase. In other cases, the vendor may discontinue certain products and introduce alternative. Search engine provide a good platform to promote or cannibalize products.

Please note that, again due to the fuzzy and subjective nature of a search engine, the best metric to track depends heavily on the business of the content provider and can be none of the above. The above examples are indicative of what a typical e-commerce vendor could consider.