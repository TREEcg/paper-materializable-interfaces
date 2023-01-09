## Building materializable interfaces
{:#method}

TODO: What is materializable → define!!!

There is undoubtedly a large number of ways in which a dataset can be fragmented, similar to the amount of indexes and summaries one can make from the same dataset.
We did not aim to design the one hypermedia specification to rule them all.
Instead we aimed to have a set of building blocks that can be used to fulfill various use cases with similar characteristics.
If they can work interchangeably, we have succeeded in creating both _reusable code_ across different Web APIs, and well as creating _evolvable_ APIs.

The TREE specification started from heterogeneous use cases that could benefit from such evolvability and code reuse.
The use cases we worked with included querying for geospatial relations, time schedules of public transit data, time series, OpenStreetMap’s road network and taxonomie swith text literals such as an address database, geonames, OpenStreetMap names or Wikidata entities.
In the rest of this chapter we shortly introduce some published use cases (as of January 2023) that use the `tree:Relations` for a specific group of features.

 1. __Replicating and synchronizing dataset copies across organizations__<br/>
in [](cite:cites lonneville2021publishing) and [](cite:cites van2022publishing), a fragmentation of a Linked Data Event Stream is proposed optimized 
 2. __Geospatial relations for route planning over road networks__<br/>
[](cite:cites delva2019client)
 3. __Time-based relations for route planning over public transit networks__<br/>
[](cite:cites rojas2022publishing)
4. __Substring-based relations for autocompletion__<br/>
[](cite:cites dedecker2021file)



In (1) The cases of [](cite:cites lonneville2021publishing) and [](cite:cites van2022publishing) show 

The route planning use case nicely illustrates the need for querying with a more open world ...
