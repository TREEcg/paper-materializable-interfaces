## State of the art
{:#sota}

The Linked Data Fragments axis ...
One of the first specifications in that realm was the Triple Pattern Fragments specification.
It was built from the perspective of building an interface that allows

{:.todo}
https://linkeddatafragments.org/publications/iswc2015-substring.pdf

Hartig et al. looked into link traversal of linked datasets by [following the HTTP identifiers of real-world objects it encounters](cite:cites hartig2009executing).
While this works in theory, it goes too slow for live Web applications in practise, as these data interfaces are not optimized for querying.
[Hydra](cite:cites lanthaler2013creating) is a domain model introduced in 2013 to bring the power of hypermedia to Linked Data based APIs.
Other work outside the Linked Data domain, such a [Hypertext Application Layer (HAL)](https://apigility.org/documentation/api-primer/halprimer) and [json:api](https://jsonapi.org/), introduced hypermedia specifications to Web APIs already before.
In all three of these cases, the hypermedia controls that would afford pruning a client’s search space are limited.
For instance, the nearest concept to the concept of a fragmentation strategy in [Hydra](http://www.hydra-cg.com/spec/latest/core/) is the concept of a [partial collection view](http://www.hydra-cg.com/spec/latest/core/#collections).
This view describes how to get to the first, next, previous or last page.
Yet, no description is provided on whether or not the view is ordered, and thus, when a smart client would visit the page, it would have to iterate across all pages for any query.
An early attempt at making a client detect automatically how to navigate further through a list or things in an ordinal range was with the [multidimensional interface specification](cite:cites mdi).

Another specification that includes hypermedia controls as part of a broaded protocols is [Activity Streams 2.0](https://www.w3.org/TR/activitystreams-core/).
This specification does allow to indicate pages are ordered, yet the description of the ordering itself is left out of scope.
[Linked Data Platform (LDP)](https://www.w3.org/TR/ldp/) is a World Wide Web (W3C) specification that also puts forward a pagination specification.
[Despite its conflicts with Hydra and Activity Streams 2.0](cite:cites mihindukulasooriyadescribing), it does put forward a way to describe how a collection is ordered.
It is the only example in the state of the art I found so far that could allow clients to effectively prune their search space to some extent. We did however not find any evidence of clients taking advantage of this specific feature.

In order to enable clients to prune their search space based on hypermedia descriptions beyond simple pagination, we need to come up with a comprehensible specification, as well as describe the client-side algorithm.
In contrast to the state of the art, we want the specification to describe precisely how the index works, so any client-side query algorithm can benefit without a human developer having to explain how to interpret the responses.
