--- 
layout: post
title: "Search Engine - Testing an implementation."
comments: true
tags:
- search
- testing
summary: "Approaches to testing a search engine implementation."
---

Testing a search engine implementation can be straightforward enough when the use cases restrict to either searching by an identifier or limited number of fields. As the search expands to fuzzy areas such as free text, the structure of data starts diluting. This makes testing a search engine increasingly complicated. After a certain point, there ceases to be one expected output to assert on.

For example, consider the below product listings

1. Apple IPhone 4s
2. High quality Screen protector for Apple IPhone 4s.

A user looking to purchase an "IPhone" will get both these listings as matches. And both of them are partial match to the title field. Which one is correct in this case?

In this case, search engines have implementations that do some text analysis to figure out the relevance score, and bring up the best textual match. However, the customization of search engines can override such analysis, and needs to be tested.

Here are some techniques that help in testing a search implementation.

**_Simple lookups_**

**Identifier based** - This is very helpful when there are documents with unique IDs indexed in the search engine, and the document IDs are also something that the users will use. All this case would require is a set of identifiers and corresponding matches that can be asserted on.

For instance, cellphone model names are something that most user will be aware of. These lookups are simple enough and can be tested quite easily. On the other hand, apparels' identifiers are rarely used by the users, so they serve very little purpose.

**One field at a time** - Besides unique identifiers, the search could involve match against a single field. Title, Brand for a product are examples when the search criteria could match only one field. These scenarios can be tested similar to above, given the predictive nature of single field matching.

The above steps will help test independent rules. In a lot of cases, these could be sufficient. But in other cases, there are often combination of rules applied. The combination can be reinforcing rules or opposing ones. Below section talks about combinations applied to search rules.

**_Combinations_**

If the search engine implements a combination of rules defining matches, the complexity of asserting the search result goes beyond a boolean value. In case of the above scenarios, the testing could include just whether the hits match the search criteria. However in case of combination of search results, the relevance, order of results etc play a much important role.

In a big dataset, this combination of multiple tests makes it increasingly difficult to cover every possible edge case. It has been observed that in such cases an iterative development benefits the testing, since each rule gets tested in isolation as well as previously applied rules. The below section on 'Iterative development and testing' discusses more about this.

**_Boosts_**

Boosting fields are necessary, since they manipulate the natural behaviour of the search engine to help tune it to custom rules. This adds another dimension to the rules. Now the rules aren't just combinations, but they also have a precedence within them.

If the number of fields that have boosts defined are few, then the number of test cases are still manageable. However with the increasing number of boosted fields, it becomes very cumbersome to come up with enough test cases that will address all the scenarios. In such cases, the alternative would be to take smaller steps and test incrementally as mentioned
below.

**_Dynamic fields_**

Dynamic fields are not so widely used, but they do exist. In cases where one needs to use dynamic fields, it is a good idea to note the rules in defining the fields, not just the data indexed in them. The fields get defined at index time, and hence are not obvious just by looking at the design time schema. Search engine implementations have made provisions such as Schema Browser that allows an administrator to take a look at the snapshot of the index, includin the dynamic fields. These serve as a mechanism to identify the preconditions of the tests.

As with the case of boost, these fields can add another dimension of complexity where the search term can potentially have a hit against a field that is not known to the person defining the schema and boost values.

**_Negative Cases_**

A good search engine does not just return good matches, it also removes noise and irrelevant results. This includes omission of false positives/negatives. In order to ensure that the implementation at hand adheres to these expectation, negative test cases play an important role. However, it is often much more complex to come up with negative test cases and expectations, and in practice, lot of implementations leave negative test cases to the judgment of the person involved, rather than coming up with rules.

**_Tools/techniques_**

_Debugging_

In order to debug a search query, the single most important factor is the relevance score that comes out of the search engine for a given dataset and query term. Most of the time the score may look obvious, but when there are boosts and dynamic fields in place, the relevance score can be tricky to infer. Debugging the query helps decipher the formula used by the search engine to compute the score and this can be quite detailed.

_Highlights_

Debug output can be quite verbose, especially when the dataset is big or the query term is very common. Highlight component is typically meant to highlight matches on a search result, so that the user can have an experience such that he/she knows where in the result, is the term queried for.

This feature can also be used to test out a search implementation. Highlight component injects span tags in the result, that can be styled so that matches stand out visually. What this also allows, is to have a html aware automation test to look for these tags and perform desired asserts.

**_Regression_**

As mentioned earlier, testing a feature/behaviour is easier compared to testing combinations. It becomes increasingly complex when working against a moving target. While there are benefits of iterative development, it is often tricky to test, since what holds true today may change very quickly. 

In order to mitigate this, one way is to maintain a suite of regression tests, that could just be a collection of all individual tests. At every change, if these tests are run, the output shall indicate if any already tested feature is broken or not. In case the feature is broken, it could be one of the two possibilitles - either the search rules have changed, or there is a genuine failure of one or more scenarios. The next step could be to ensure that the tests and code are updated to meet all the regression criteria.

**Iterative development and testing**

Why?

The number of cases to be tested gets distributed across the span of development

Regression testing is continuous, changing/adding/removing one rule can be immediately tested for impact.

So why not do it in all cases?

While it looks tempting to propose this model as the de-facto search test methodology, it comes at a cost. Analyzing the data and choosing the right training set could be a daunting task, particularly when the dataset is large and complex.

**_choosing a training set_**

A training set is a subset of actual data, that can be used to run the rules and verify behaviour.

Some requirements for choosing a training set are

- good representation of actual data
- Right size : is small enough for a tester to be able to handle, andis big enough so that ripple effect can be simulated

The consequences of choosing a bad training set is something that is beaten down in any machine learning course, and I'll restrain from detailing them out here.

_Implementing using a training set_

- Step 1: Model the search engine schema using a training set
- Step 2: Make sure all rules are satisfied independently.
- Step 3: Combinations of the rules are also tested, and schema refined until all the conditions are satisfactory

The training set and search engine rules can help identify the below parameters that are required to model the Search engine schema:

- fields to be indexed
- analyzers
- tokenizers

Once these are identified, and the schema is ready, the next step is to choose various test datasets and verify for validity.

**The iteration**

Pass n: run rules -> anomalies -> tweak rules & schema -> regression -> Pass (n+1)