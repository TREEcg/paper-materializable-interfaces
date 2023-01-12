## Conclusion
{:#conclusion}

In this paper, although it was already used in previous academic work, we introduced the TREE hypermedia specification for building materializable interfaces.
We chose the term _materializable_ as it does not need to be materialized on disk, but it can be as there is only a finite set of HTTP requests that give a result.
Hosting a materializable interface should be possible with almost neglectible hosting costs.
The largest costs should come from the computational power needed to create and update a page from an interface.

This turns the four limitations of more complex query patterns in the introduction into the advantages of materializable interfaces:

 1. __You can query your end-user’s world__<br/>
Materializable interfaces assume user agents take part in the query evaluation.
That way, it can execute the queries by taking into account data that lives on the user agent’s infrastructure, with access to datasets the end-user has access to. Take for example the use case of route planning: it can take into account their home address, the fact their bike is parked in a certain location, the fact they are in a wheelchair, etc. Personalization can happen without having to build a profile on a remote server.
 2. __It becomes possible to archive an interface, not just the data__<br/>
 When a server is being decomissioned, an archiving project can traverse the hypermedia links until it replicated all pages to an archive server, and keep the files available and discoverable. That way, even after a server or even publisher disappeared, clients that relied on a certain fragmentation for their functionality can keep on working.
 3. __Evolvability can be realized through discovery on multiple levels__<br/>
 Different levels of discoverability could be coded against, that wil come with more _evolvability_.
 One idea is to have the start fragment of the specific Web API hardcoded. That way, if the structure of the hypermedia changes, it will always start again from the root of the search space.
 A higher level of evolvability can be achieved when not the URL of the Web API is hardcoded, but the ones of the dataset and a data catalog. That way, through the data catalog, all Web APIs can be discovered that publish the dataset. If one Web API is decommissioned, the user agent can fall back to another Web API publishing the same data. An even higher level of discovery could yet again be achieved by also implementing discovery on the dataset level, to, through the SHACL shape documented with the `tree:Collection`, and the provenance information attached to it, select these sources that will return an answer to a question.
 4. __Queries can be kept private__<br/>
The only thing a server sees is that a client is interested in a page of its dataset. It does not see how the query is executed and what the final recommendation or query result provided to the user is. This in stark contrast with Web APIs with URL patterns like `https://your-domain/weather{?long,lat}` that would be polled for weather information.

## Future work
{:#future-work}

The current version of the TREE vocabulary has been submitted to [LOV](cite:cites lov).
In order to further evolve the specification, we are now starting a TREE/LDES community group at W3C for which we are now seeking support.

The last information on the TREE hypermedia project can be found at [https://tree.linkeddatafragments.org](https://tree.linkeddatafragments.org).
In future work, we are also going to tackle graph-based and time series fragmentations with the TREE/LDES method.
Furthermore, the [Comunica Querying engine](cite:cites taelman_iswc_resources_comunica_2018) is being extended with a TREE hypermedia querying actor that does query planning across multiple hypermedia interfaces.

