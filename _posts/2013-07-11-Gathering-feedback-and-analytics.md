--- 
layout: post
title: "Search Engine - Gathering feedback and intelligence."
comments: true
tags:
- search
summary: "Approaches to inferring intelligence from a search engine."
---

A lot of search implementations are straightforward, while a lot others aren't. The previous set of posts illustrate that it takes much more than a tool to get the right search engine in place. And quite often, the implementors do not get the right formula in the first shot.

An important aspect of search engines (or any system, for that matter) is feedback. The success or failure depends on whether it meets or exceeds the user's expectation.

This is an attempt to illustrate various aspects that can be inferred by looking at feedback from users. In this case, these are categorized as Supervised and Unsupervised (borrowed from machine learning theory).

**Supervised**

This class of feedback are something that the user can give explicitly. These are simpler to implement (as simple as asking the user). Some examples are -

1. User suggestion - If the user tries searching and the search engine returns no results, the user could suggest that the producer include such product/content in the catalog.

2. User rating - At every search result, the website could ask the users if they found what they were looking for and capture various attributes such as ease of use etc.

**Unsupervised**

These are slightly trickier to implement, but are un-intrusive to the user. The trick is to watch the usage and infer performance of the system by comparing it with benchmarks or pre-defined goals.

Some examples are -

1. Refined searches - How many searches have caused the user to make an attempt to refine the search terms?
2. No result found - How many search results yield no results? Is the search term too specific or is there scope for tuning?
3. Add synonyms - How do the users see product/content, and compare it to the publisher's definition.
4. Enrich data - Push the product definition such that the best matches start surfacing on top. (More in the next section)
5. Paginated? Page number clicked - This could be a measure of relevance - how many times do the users move to pages till they reach the right results? This implies that in these cases, the relevance isn't matching the user's expectation.

**Means to infer these feedback**

The logs are source of the real truth, on how the users use the website for search. It is possible to analyze the logs to identify search patterns and come up with rules that could be fed back to the search engine. 

Some possibilities are that logs can extend support :

Looking at the refinement rate could identify keywords that have gaps between what the users want and what the system provides. The feedback in this case could be

- areas that need to be enriched.
- add synonyms/tags or any other form of metadata to the products.
- Combining search results with something like google analytics could help identify false matches. _This is more likely to be a case of bad data rather than poor search engine implementation. If it were poor implementation of search engine, then there would be a clear pattern (including both false positives as well as false negatives) as opposed to odd cases._




