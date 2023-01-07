## Introduction
{:#introduction}

The Web is a global information system that makes representations of resources addressable using URLs.
While the most visible use case to end-users is using URLs to address websites and their pages in their browser, developers also use exactly the same technique in what they call Web APIs to share data between user agents.
Just like a website, not all content or data that is managed through one server is exposed via only one resource.
Instead, a Web API is a resource structure that exposes one or more views over the collection of data.

Depending on how tightly coupled the user-agent application and the Web API are, designing the resource structure of the Web API becomes more or less straightforward.
I.e. if there is only one app that needs the data the API exposes, and both are controlled by the same developer, the resource structure can be driven by exactly the user stories of the app itself.
However, if an unknown number of potential systems need to be able to reuse the data, such as it is the case when designing APIs for Open Data publishing, or resource structures within [the Solid project](https://solidproject.org/), it becomes guess-work on what API will work best. <!-- REREAD THIS POINT: does it make clear that the use cases here is using servers that you don’t control, so that need a fixed spec you can use? -->

[The Linked Data Fragments (LDF) axis](cite:cites verborgh_jws_2016) for building Web APIs describes two extremes: i) either the user agent downloads the full dataset and performs all processing on their infrastructure, ii) either the server creates an ad-hoc resource that gives precisely the data the user agent wants based on a query that is sent to the server.
Examples of the latter include the SPARQL protocol for querying RDF data, but equally, GraphQL, a full-text search API or a geospatial Web Feature Service (WFS) would be good examples.
These specifications allow almost any flexibility to be given to the user agent developer to formulate any possible query.
However, creating ad-hoc resources answering the full query on a server poses four important problems:

 1. __Querying a closed world__: You only query the data integrated on the machine you query. This can be problematic in case you do not control the server you want to query, as it would not have the features or all data you need for your use case.
 2. __Evolvability__: coding against a purpose-built protocol lowers potential evolvability.
 3. __Archiving__: relying on dynamic server functionality raises challenges in long-term preservation.
 4. __Privacy__: sending the full query to a third party server lowers query privacy.

These two extremes are positioned as a false dichotomy by LDF.
If the user agent can take up more responsibility in the query processing, then more options come to exist.
If the initial dataset is 

The idea is further extended by [Linked Data Event Streams (LDES)](cite:cites ldes).
LDES positions the ideal Web API view on top of a dataset does not exist,
and thus the dataset itself will always be published through __multiple views__.
This means, the first priority when sharing a dataset should 

LDES is introduced as a vocabulary to indicate an append-only log of updates to 
Using LDES, multiple views can be built 
We will work on hypermedia specification



<!--

<figure id="architecture">
<img src="https://docs.google.com/drawings/d/e/2PACX-1vTclSwOAzLFmdR9Q_wtQPleN_CU767ZdWax9bkOWZk7h5dWf5zoIYz-0u-bKvV8Q-Bxzo5o9erWU5kO/pub?w=951&h=482" alt="The architecture of LDES, materializable interfaces"></img>
<figcaption markdown="block">
Architecture
</figcaption>
</figure>
-->
