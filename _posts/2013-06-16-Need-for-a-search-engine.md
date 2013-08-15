--- 
layout: post
title: "Search Engine - Need for a custom search engine"
comments: true
tags:
- search
summary: "Some ideas on points to note when deciding a search engine implementation."
---

A lot of websites today have a search box somewhere. A few of them get it right, most of them do not. This is one reason why many people prefer Search Engines such as Google to get to whatever they want. Another reason is aggregated results - search engine results provide options to the users which most websites cannot. As a customer, it is fair to expect that one should be given the best search result to the requirement one has, not constrained by provider's capability.

However, as a merchant/provider there are enough reasons to have a search engine within the website. But, if as a provider one chooses to take on search engine giants, the task becomes increasingly daunting. Also in which case, to a user using a vendor's search would mean restricting oneself to whatever the vendor has to offer, which could be a fair assumption in a minority of cases (I speculate here, this highly depends on the market share the vendor holds, products that are niche to a vendor etc.,  factors, but my speculation could be applied to general commodity e-commerce vendors).

So, before taking on the task of implementing a Search Engine in a website, it's always good to understand the motive and benefits. 

###Benefits of a Need Analysis

- Understand the primary and secondary objectives.
- Helps formulate goals against which the implementation can be measured

The above points are applicable to cases beyond Search Engine. But, in this case, the search results are sometimes[beyond simple text match]({% post_url 2013-07-05-Beyond-simple-text-match %}).

As with most projects, there should be a driving need behind implementing a Search Engine. It is worth repeating here that most websites could not benefit much by competing against Search Engine, unless they have the time, resource and vision to take them on. Most vendor site's core business isn't Site Search, but a good search engine can boost the reach of the products/content to the user. 

###What is the purpose of Search Engine in your website?

There could be multiple reasons, not necessarily exclusive. One way to reach to this conclusion is to do a bit of [Gap Analysis](http://en.wikipedia.org/wiki/Gap_analysis). The actual analysis strategy could be defined case by case. 

####An Example
A product vendor could look at the keywords/context that the users search and look to see if there are products/contents matching. A good sample set for this analysis should surface some patterns that have been missed at the current state. 

Note that, the gap identified could be because of two reasons -

1. The product/content that the user is looking for doesn't exist in the vendor's domain
2. The product/content exists in the vendor's domain, but the user's way of looking for it is significantly different from the way the vendor defines it.

For (1) there is little the Search Engine can do, besides acting as a feedback to the vendor to possibly expand the product/content catalog.

(2) is where a Search Engine can act as a bridge that translates the vendor's definition to what a user would understand.

###Benefits

- Reach products/ pages in the website in the most intuitive way
- Serve as a platform for exploration, thereby getting the users to spend more time on the website

The first case is the default use case for most websites that use a search engine such as [Apache Solr](http://lucene.apache.org/solr/). One could simply wire up a Solr instance with a data-store and get up and could benefit from the quick lookup.

In the second scenario, the focus is towards creating navigated paths or journeys for the users to sift through a wide catalog of products or pages and lead them to something of specific interest. A search engine such as Solr has a good set of features as well as an ecosystem of plugins that can support features like Faceted Navigation which help increase the browse experience of the user.

It might be worth considering if a custom search engine could serve complementing purpose to search engines such as Google. An example would be to define custom landing pages for products powered by Facets. If there are enough links around, search engines could then surface them to the relevant searches.

