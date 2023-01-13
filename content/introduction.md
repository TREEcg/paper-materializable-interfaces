## Introduction
{:#introduction}

The Web is a global information system that makes representations of resources addressable using URLs.
While the most visible use case to end-users is using URLs to address websites and their pages in their browser, developers also use exactly the same technique in what they call Web APIs to share data between user agents.
Just like a website, not all content or data that is managed through one server is exposed via only one resource.
Instead, a Web API is a resource structure that exposes one or more views over the collection of data.

<figure id="url-pattern" class="listing"  markdown="block">
```
https://your-domain/your/resource/structure{?parameters}
```
<figcaption markdown="block">
Organizations build their own resource structure based on protocols they want to follow.
</figcaption>
</figure>

Depending on how tightly coupled the user-agent application and the Web API are, designing the resource structure of the Web API becomes more or less straightforward.
I.e. if there is only one app that needs the data the API exposes, and both are controlled by the same developer, the resource structure can be driven by exactly the user stories of the app itself.
However, if an unknown number of potential systems need to be able to reuse the data, such as it is the case when designing APIs for Open Data publishing, or resource structures within [the Solid project](https://solidproject.org/), it becomes guess-work on what API will work best. <!-- REREAD THIS POINT: does it make clear that the use cases here is using servers that you don’t control, so that need a fixed spec you can use? -->

[The Linked Data Fragments (LDF) axis](cite:cites verborgh_jws_2016) for building Web APIs describes two extremes: i) either the user agent downloads the full dataset and performs all processing on their infrastructure, ii) either the server creates an ad-hoc resource that gives precisely the data the user agent wants based on a query that is sent to the server.
Examples of the latter include the SPARQL protocol for querying RDF data, but equally as well, GraphQL, a full-text search API or a geospatial Web Feature Service (WFS).
These specifications allow almost any flexibility to be given to the user agent developer to formulate any possible query.
However, creating ad-hoc resources answering the full query on a server poses four important limitations:

 1. __You are querying a closed world__<br/>
You only query the data integrated on the machine you query. This will thus not be a good solution for cases in which you do not control the server you want to query: it could not have the features or data you need for your use case.
 2. __It is challenging to archive__<br/>
 Relying on dynamic server functionality raises challenges in long-term preservation.
 When the amount of different queries you can ask the server is infinite, what queries will you archive?
 3. __It is difficult to turn off or evolve an API once it has been made available__<br/>
 Coding against a purpose-built protocol lowers the potential evolvability of that API.
 Turning off this API in favour of a different specific Web API with ad-hoc resources built based on a specific language will require applications to be recoded towards that novel specification.
 4. __It leaks query privacy__<br/>
Sending the full query to a third party server shares the full questions your users are interested in to that server.

These two extremes are positioned as a false dichotomy by LDF.
If the user agent and the initial server can take up more responsibility in the query processing, then more options come to exist.
A dataset that is too big for one page can be _fragmented_ according to a certain property in the data, and therefore, by documenting the property, can help the user agent in pruning what fragments it needs to download in order to answer a certain query. 

The idea is further extended by [Linked Data Event Streams (LDES)](cite:cites ldes).
LDES further reasons the ideal Web API on top of a dataset does not exist, as any type of fragmentation will introduce bias towards a specific use case.
Therefore, a dataset will be published through __multiple Web APIs__ as illustrated in [](#multiple-views), and not just one, managed by multiple organizations using multiple Web servers.
LDES continues by then positioning that, if multiple views must become possible, that the first Web API a data publisher should build, is an event source, that focuses on keeping derived Web APIs in-sync with its authoritative source over the Web.

<figure id="multiple-views">
<img src="https://docs.google.com/drawings/d/e/2PACX-1vRoAoYfTvy7l8EJA7KIZGMCsj8BWgxyqYBgniHqOGNhEowjZb6Br1RSmMyGG0MEjmG7D7zY5D0ZUiNN/pub?w=890&h=311" alt=""/>
<figcaption>The same dataset will be published on the Web using multiple interfaces.</figcaption>
</figure>

In this paper, we look into making these event sources and derived Web APIs evolvable and preservable, and mitigate the four limitations mentioned above.
Even when a service or dataset is decommissioned, user agents that were once built on top of it, will still be able to resolve queries against archived data.
In [](#results), we sketch our first steps into designing the TREE specification for guiding user agents through a fragmented dataset.
In [](#method), we then show using a couple of examples how to build what we will call _materializable_ Web APIs.
Finally, in [the Conclusion](#conclusion), we reiterate the limitations and discuss how these materializable Web APIs tackle them.
