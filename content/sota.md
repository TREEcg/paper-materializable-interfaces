## State of the art
{:#sota}

Hartig et al. looked into Link Traversal Query Processing by [following the HTTP identifiers it encounters in the triples of Linked Data documents](cite:cites hartig2009executing).
While this works, as also implemented [in Comunica](https://comunica.dev/research/link_traversal/) [](cite:cites taelman_iswc_resources_comunica_2018), it goes too slow for live Web applications in practice, as these data interfaces are not optimized for querying.
In our work, we will look into more directed link traversal, by making the data publishing include explicit hypermedia controls into their results.

<!--
[Triple Pattern Fragments](cite:cites verborgh_jws_2016) proposed to limit the server’s capabilities to only answering triple patterns, the most basic question you can ask to an RDF triple store.
This translates into a relatively simple URL pattern compared to the full SPARQL query language, as illustrated in [](#url-pattern-2).
The interesting idea behind this system is that it does not only allow triple patterns to be answered by user agents, but also full Basic Graph Patterns by performing the join on the infrastructure of the user agent.
The paper showed remarkable results: some SPARQL queries would show the first results even faster than the state of the art in SPARQL endpoints.
Further work then tried to extend the interface with more dynamic server features, such as [filtering based on substring](van2015substring) or binding restricted triple pattern fragments
In this paper we instead propose 

<figure markdown="block" class="listing" id="url-pattern-2">
```
https://your-domain/your/dataset{?subject,predicate,object}
```
<figcaption>
The resource structure proposed by Triple Pattern Fragments. The page will return the answer to the triple pattern, and hypermedia controls to navigate further through the dataset.
</figcaption>
</figure>
-->

[Hydra](cite:cites lanthaler2013creating) is a domain model introduced in 2013 to bring the power of hypermedia to Linked Data based APIs.
Other work outside the Linked Data domain, such a [Hypertext Application Layer (HAL)](https://apigility.org/documentation/api-primer/halprimer) and [json:api](https://jsonapi.org/), also introduced hypermedia specifications to Web APIs.
In all three of these cases, the hypermedia controls that would afford pruning a client’s search space are limited.
For instance, the nearest concept to the concept of a fragmentation strategy in [Hydra](http://www.hydra-cg.com/spec/latest/core/) is the concept of a [partial collection view](http://www.hydra-cg.com/spec/latest/core/#collections).
This view describes how to get to the first, next, previous or last page.
Yet, no description is provided on whether or not the view is ordered, and thus, when a smart client would visit the page, it would have to iterate across all pages for any query.

Another specification that includes hypermedia controls as part of a broaded protocols is [Activity Streams 2.0](https://www.w3.org/TR/activitystreams-core/).
This specification does allow to indicate pages are ordered, yet the description of the ordering itself is left out of scope.
[Linked Data Platform (LDP)](https://www.w3.org/TR/ldp/) is a World Wide Web (W3C) specification that in an extension also puts forward a [paging specification](https://www.w3.org/TR/ldp-paging/).
[Despite its conflicts with Hydra and Activity Streams 2.0](cite:cites mihindukulasooriyadescribing), it does put forward a way to describe how a collection is ordered.
It is the only example in the state of the art we found so far that could allow clients to effectively prune their search space to some extent. We did however not find any evidence of clients taking advantage of this specific feature.

In order to enable clients to prune their search space based on hypermedia descriptions beyond simple pagination, we need to come up with a comprehensible specification, as well as describe the client-side algorithm.
An early attempt at making a client detect automatically how to navigate further through a list or things in an ordinal range was with the [multidimensional interface specification](cite:cites mdi).

In contrast to the state of the art, we want the specification to describe precisely how the index works, so any client-side query algorithm can benefit without a human developer having to explain how to interpret the responses.

